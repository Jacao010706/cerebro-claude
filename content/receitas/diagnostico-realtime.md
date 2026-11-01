# Diagnóstico — o Realtime está funcionando?

Meça antes de supor. Um dia inteiro já se perdeu com hipóteses
plausíveis e erradas; as respostas vieram dos logs.

> **Fuso:** os logs do Supabase são em **UTC**. Horário de Brasília + 3 h.
> Já houve consulta a uma janela no futuro por causa disso.

## O navegador está conectando?

```sql
SELECT formatDateTime(timestamp,'%H:%i:%S') AS hora_utc,
       log_attributes['response.status_code'] AS status
FROM logs WHERE source='edge_logs'
  AND log_attributes['request.path']='/realtime/v1/websocket'
ORDER BY timestamp DESC LIMIT 10
```

| Resultado | Significa |
|---|---|
| `101` | Conectado |
| `401` | Chave recusada — ver [[armadilhas/supabase-realtime]] |
| nada | O cliente nem tentou: variável faltando no build |

## Alguma coisa está gravando?

```sql
SELECT log_attributes['request.method'] AS metodo,
       log_attributes['request.path'] AS caminho,
       log_attributes['response.status_code'] AS status,
       count(*) AS n
FROM logs WHERE source='edge_logs'
GROUP BY metodo, caminho, status ORDER BY n DESC
```

Zero linhas em `/rest/v1/` significa que a chamada **nem sai** — não é
falha de gravação.

## No navegador, sem depender de timing

`F12` → aba **Rede** → botão **Socket** (é assim que o Edge em português
chama o filtro WS) → `F5`. Procure `supabase.co` com status 101.

**Desligue o filtro Socket depois.** Esquecido, ele faz parecer que não
existe requisição nenhuma — isso já gerou um diagnóstico errado.

## O painel degradou para polling?

Console do navegador, filtro `CCO`. Se aparecer
`[CCO] Supabase nao configurado`, as variáveis não chegaram ao build.

## Teste manual, com o polling desligado

Localmente, troque `setInterval(loadAll, 30_000)` por `600_000` para o
push ficar na tela em vez de ser sobrescrito em 30 s. Depois volte.
