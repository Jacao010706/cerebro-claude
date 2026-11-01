# Diagnóstico — de onde vem esse 404?

## As rotas `/api/v1/*` são proxies

Elas não consultam banco. Chamam `backendFetch()` no FastAPI e
**repassam o status do backend**. Um 404 vindo do Python aparece como
404 da rota local — e faz procurar o defeito no lugar errado.

## Verifique as três variáveis primeiro

```powershell
Get-Content .env.local | ForEach-Object { ($_ -split '=')[0] }
```

Devem existir `BACKEND_URL`, `BACKEND_EMAIL`, `BACKEND_PASSWORD`.
Sem as duas últimas, `getServiceToken()` devolve `null`, a requisição sai
sem `Authorization` e o backend recusa.

## Confirme o que a página realmente chama

`F12` → aba **Rede** → clique em **Tudo** (desligue filtros de tipo) →
digite o nome da rota no filtro de texto → `F5`.

Se a chamada **não aparece**, o código não está chegando naquela linha.
Se aparece com status, o status diz de quem é a culpa.

## O log do dev server só existe em desenvolvimento

`npm run dev` registra cada requisição. `next start` em produção não.
A ausência de linhas no log de produção **não** prova que a chamada não
aconteceu.
