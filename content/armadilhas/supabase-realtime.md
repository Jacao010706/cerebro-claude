# Supabase Realtime — a chave precisa ser JWT

## Sintoma

O navegador tenta conectar de 10 em 10 segundos e o Supabase responde
**401** em `/realtime/v1/websocket`. O painel funciona normalmente, mas
sem tempo real.

## Causa

O Realtime só aceita chave em **formato JWT**.

| Chave | Formato | Realtime |
|---|---|---|
| `anon` (`eyJ...`) | JWT | ✅ conecta, status 101 |
| `sb_publishable_...` | não-JWT | ❌ recusada, 401 |

A chave publicável é mais moderna e mais fácil de rotacionar, mas **não
serve** para o Realtime.

## Solução

Use a chave `anon` em `NEXT_PUBLIC_SUPABASE_ANON_KEY`.

Como ela é longa (200+ caracteres), cuidado com o truncamento ao colar —
ver [[armadilhas/deploy-railway]].

## Como confirmar

Ver [[receitas/diagnostico-realtime]].
