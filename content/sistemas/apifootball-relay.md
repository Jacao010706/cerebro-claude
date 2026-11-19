---
tags: [simanplay, sistemas]
---

# apifootball-relay (aba Jogos)

Criado em 16/11/2026. Faz o backend do SimanPlay chamar a API-Football
**saindo pelo IP fixo do VPS**, e não pelo IP compartilhado do Railway.

## Por quê

A conta grátis da API-Football (api-sports.io) foi **suspensa** em nov/2026.
O painel mostrava **0% usado** — não era cota. O suporte confirmou: IP
compartilhado do Railway sinalizado por uso de outros clientes. A solução
recomendada por eles é IP dedicado. Ver [[decisoes/2026-11-16-apifootball-via-vps]].

## Como funciona

- Código: `/root/apifootball-relay/server.js`, systemd `apifootball-relay`,
  só em `127.0.0.1:3003`.
- Caddy: `proxy.sofae.com.br/apifootball/*` → `localhost:3003`.
- Só aceita `GET` em `/fixtures` e `/status`, exige header `X-Relay-Secret`,
  limite de 30 pedidos/min. Repassa o `x-apisports-key` que vem do backend
  (a chave **não** fica no VPS).
- Log: só caminho, status, campo `errors` e número de resultados. Nunca chave/senha.
- Senha do repasse: `/etc/apifootball-relay.env` (permissão 600) e no Railway.

## Backend (única mudança autorizada no backend)

- `sports.py`, commit `fb623f7` na `main` do backend (16/11).
- Lê `API_FOOTBALL_BASE_URL` (padrão: endereço original) e
  `API_FOOTBALL_RELAY_SECRET` (se existir, manda `X-Relay-Secret`).
- **Sem as duas variáveis, o comportamento é o de antes.** Para voltar atrás:
  apagar as variáveis no Railway (serviço `web`, aba Variables).
- No Railway: `API_FOOTBALL_BASE_URL=https://proxy.sofae.com.br/apifootball`
  e `API_FOOTBALL_RELAY_SECRET` (valor no `.env` do VPS).

## Respostas do `/sports/fixtures`

| Status | Significado |
|---|---|
| 503 | `API_FOOTBALL_KEY` vazia |
| 403 | data fora do plano |
| 502 | qualquer outra falha (chave inválida, conta suspensa, limite) |

Cache: 30 min (hoje) / 6 h (outras datas).

## Estado em 19/11 — funcionando

- A conta antiga continua suspensa. **Conta nova** (grátis, 100 pedidos/dia)
  criada em 19/11 com outro e-mail; a chave nova está no Railway
  (`API_FOOTBALL_KEY`, serviço `web`) — nunca aqui.
- Testada pelo VPS (`/status` → `"errors":[]`, plano Free ativo) e pelo
  backend: `/sports/fixtures` voltou com jogos e escudos.
- **Não usar a conta antiga em lugar nenhum**: todos os pedidos saem só pelo
  IP do VPS.
- Uso diário: conferir em dashboard.api-football.com. O cache do backend
  (30 min hoje / 6 h outras datas) segura o consumo.
- O campo `emissoras` vem vazio: a API-Football não informa o canal.

### Testes rápidos (terminal do VPS)

```bash
# conta/chave (a chave não aparece na tela)
read -s K; curl -s -H "x-apisports-key: $K" https://v3.football.api-sports.io/status; echo; unset K
# últimos pedidos que passaram pelo repasse
journalctl -u apifootball-relay -n 5 --no-pager
```

## Histórico (18/11)

- Repasse funcionando, mas a conta antiga seguia suspensa.
- Atendimento humano do chat da API-Football: seg–sex, 7h–16h UTC
  (4h–13h de Brasília), botão "Chat with an agent".
- "Allowed IPs" no painel deles só funciona em plano pago.
- Alternativa paga: plano Pro (~US$ 19/mês, 7.500 pedidos/dia).
