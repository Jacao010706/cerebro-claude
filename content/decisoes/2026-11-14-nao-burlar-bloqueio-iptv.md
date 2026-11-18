---
tags: [sofae, decisoes]
---

# 2026-11-14 — Não burlar o bloqueio do provedor IPTV

## Decisão

Não repassar o IP do cliente (`X-Forwarded-For` / `X-Real-IP`) no proxy
para o provedor achar que a conexão vem de casa. A web não toca canais ao
vivo desse provedor; o caminho é o app nativo.

## Por quê

- O provedor bloqueia datacenter **de propósito**. Contornar é burlar um
  controle de acesso que ele colocou.
- Risco de banir a linha (várias conexões "residenciais" saindo do mesmo IP).
- O Sofae se apresenta como "apenas um player"; burlar o provedor tira essa
  posição neutra — e é exatamente o que as lojas olham.
- O próprio filtro de segurança da sessão marcou o pedido.

## Consequências

- Web: depois de 20 s ou de falhar, mensagem "o seu provedor só libera
  canais ao vivo direto do seu aparelho" + botão "Baixar o app Sofae".
- Apps nativos em todas as plataformas (a ideia do Windows veio daqui: o
  Zuxo no PC é app da Microsoft Store, não site).
