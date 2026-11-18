# sofae-proxy (proxy de streams do web app)

Criado em 13/11/2026 para o web app do [[sofae]] tocar canais ao vivo.

- Código: `/root/sofae-proxy/server.js` (Node, sem dependências).
- Serviço: `systemctl status sofae-proxy` (escuta só em `127.0.0.1:3002`).
- Exposto por Caddy em `https://proxy.sofae.com.br/stream?url=<url codificada>`.
- `GET /health` responde ok.

## Proteções

- CORS só para `https://app.sofae.com.br`; sem `Origin` → 403.
- Bloqueia IPs internos depois de resolver o DNS (anti-SSRF).
- Não grava URL em log (as URLs têm usuário e senha da lista).
- Reescreve playlists HLS: segmentos também passam pelo proxy.

## Por que ele não resolveu o problema

O provedor de teste recusa **qualquer IP de datacenter** no endpoint de
stream (401), inclusive este VPS. Ver [[armadilhas/iptv-bloqueia-datacenter]].
O proxy continua ligado porque serve para provedores que não bloqueiam.
Para desligar e economizar memória: `systemctl disable --now sofae-proxy`.

## Ordem de tentativas no `js/player.js` da web

1. URL direta (só se for `https://`)
2. VPS (`proxy.sofae.com.br/stream`)
3. Vercel (`/api/proxy`) — reserva

Erro fatal nos segmentos agora avança para a próxima tentativa (antes
ficava em loop de `startLoad()` e "Carregando..." infinito).
