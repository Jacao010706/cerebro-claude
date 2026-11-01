# Railway

## Serviços do projeto SGM

| Serviço | Papel |
|---|---|
| `sgm-geradores-trensurb` | Frontend Next.js |
| `daring-vitality` | (a documentar) |
| Postgres | Banco de produção |

## Variáveis do serviço Next.js

| Variável | Para quê |
|---|---|
| `BACKEND_URL` | Endereço do FastAPI |
| `BACKEND_EMAIL` / `BACKEND_PASSWORD` | Token de serviço para o FastAPI |
| `JWT_SECRET` | Assinatura dos tokens |
| `DATABASE_URL` | Referência `${{Postgres.DATABASE_URL}}` |
| `SUPABASE_URL` / `SUPABASE_SERVICE_ROLE_KEY` | Espelho no servidor |
| `NEXT_PUBLIC_SUPABASE_URL` / `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Realtime no navegador |
| `VAPID_*` | Notificações push |

## Conexão ao Postgres de fora do Railway

Use `DATABASE_PUBLIC_URL`, não `DATABASE_URL`. A comum aponta para
`postgres.railway.internal`, endereço que só existe dentro do Railway.

## Sem Alembic

Mudanças de schema vão por `ALTER TABLE` direto, pela aba Query do
dashboard. Não use PowerShell para isso.

## Ver também

[[armadilhas/deploy-railway]]
