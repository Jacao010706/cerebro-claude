# Supabase

Projeto `yzfmcbstbkglrmbilhbz`. Região **us-west-2** (não é São Paulo).
Organização `akitemtech`, plano free.

Adotado em setembro de 2026 **ao lado** do Railway, não no lugar dele.

## Tabela `iot_readings`

Cópia fiel do schema que o `route.ts` cria no Railway, para que migrar o
banco depois não exija reescrever nada.

```sql
sublocal   TEXT PRIMARY KEY
readings   JSONB NOT NULL DEFAULT '{}'
status_com TEXT NOT NULL DEFAULT 'Desconectado'
updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
```

Com `REPLICA IDENTITY FULL`, na publicação `supabase_realtime`, RLS
ligado e **uma** policy: `SELECT` para `anon` e `authenticated`.
Escrita pelo navegador é recusada.

## Storage

`os-fotos` (10 MB/arquivo) e `os-anexos` (25 MB), ambos **privados**.
O backend gera URL assinada de 1 hora sob demanda.

Convive com o Cloudinary: anexos antigos mantêm `provider='cloudinary'`;
novos gravam `provider='supabase'` + `storage_path`.

## RLS nas demais tabelas

Todas com RLS ligado e **sem policy** — invisíveis para a chave `anon`.

Isso é proposital: o painel CCO é público e carrega a chave `anon` no
navegador. A tabela `assets` guarda os IPs `10.80.0.x` e os `slave_id`;
ela nunca pode responder à chave pública.

## Onde achar as chaves

Painel do Supabase → Settings → API Keys.
Nunca registre o valor delas aqui.

## Ver também

[[armadilhas/supabase-realtime]] · [[receitas/diagnostico-realtime]]
