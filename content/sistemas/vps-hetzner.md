# VPS Hetzner

Servidor Ubuntu (`ubuntu-4gb-nbg1-1`, 4 GB, Alemanha/Nuremberg).
IP: ver painel da Hetzner. Login root: senha redefinida pelo Rescue em 13/11
(ver gerenciador de senhas, nunca aqui).

## O que roda nele

| Pasta / serviço | O que é | Como roda |
|---|---|---|
| `/root/sofae-webapp` | código do web app do [[sofae]] | deploy manual `vercel --prod` |
| `/root/sofae-proxy` | proxy de streams IPTV (porta 3002, só `127.0.0.1`) | systemd `sofae-proxy` |
| `/root/apifootball-relay` | repasse da API-Football (porta 3003, só `127.0.0.1`) | systemd `apifootball-relay` |
| `/root/simanplay-iptv-whatsapp` | bot de WhatsApp | pm2 |
| `/root/sofae-windows-build` | cópia do app Flutter (branch `sofae-windows`) | — |
| `/root/sofae-loja-build` | cópia do app Flutter (branch `sofae-loja`) | — |
| `/root/flutter-sdk` | Flutter para rodar testes | — |
| `/root/cerebro-claude` | este cofre | — |
| pastas **protegidas** | `simanplay-iptv-app`, `simanplay-iptv-backend`, `simanplay-iptv-admin-panel`, `sgm-ferroviario`, `sgm-geradores` | não mexer sem autorização |

## Caddy (HTTPS)

- `/etc/caddy/Caddyfile`: bloco `proxy.sofae.com.br` → `localhost:3002`,
  com a rota `/apifootball/*` → `localhost:3003`. O bloco `:80` original foi mantido.
- Certificado automático (Let's Encrypt). DNS `proxy.sofae.com.br` é registro A
  no Registro.br apontando para o VPS.
- Antes de mexer: backup do Caddyfile + `caddy validate`.

## Memória

- 4 GB e **sem swap** até 16/11 → o kernel matava processos (OOM): já
  derrubou o `sofae-proxy` e o Chrome. Em 16/11 foi criado **swap de 2 GB**
  (`/swapfile`, no `/etc/fstab`).
- O que mais pesa: servidor do VS Code Remote (uma cópia por reconexão,
  ~350 MB cada) e Claude Code. Para limpar: **Ctrl+Shift+P → Kill VS Code
  Server on Host**.
- Duas sessões antigas do `claude` em tmux (desde 31/10) foram fechadas em 16/11.
- Testes do Flutter no VPS: rodar **um arquivo por vez** (a suíte inteira
  estoura a memória). A suíte completa roda no GitHub Actions.

## Como acessar

1. **VS Code Remote-SSH** (`vps-hetzner`) — o jeito certo. Terminal com teclado normal.
2. Console web da Hetzner — só emergência. Ver [[armadilhas/console-hetzner-teclado]].
3. Claude Code dentro do VS Code remoto — logar com a **assinatura**, não
   com chave de API. Ver [[armadilhas/claude-code-api-key]].

## Ver também

[[sistemas/sofae-proxy]] · [[sistemas/apifootball-relay]]
