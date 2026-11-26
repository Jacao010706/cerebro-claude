---
tags: [sofae, decisoes]
---

# 2026-11-25 — Sofae nas TVs Samsung e LG pelo Media Station X

## Decisão
Levar o Sofae para Smart TVs Samsung e LG pelo **Media Station X** (app gratuito
das lojas das TVs), com um plugin nosso em `sofae.com.br/msx/`, em vez de fazer
app próprio em Tizen e webOS.

## Por quê
- **Sem certificação** da Samsung e da LG, e um único código para as duas marcas.
- O vídeo e o catálogo vêm **direto do provedor, pela internet da casa do cliente** —
  respeita [[decisoes/2026-11-14-nao-burlar-bloqueio-iptv]] (nada passa pelo datacenter).
- Reaproveita a licença do app Android (7 dias grátis + renovação) sem mexer no backend.
- O Zuxo já usa esse caminho (`zplay.top`) com sucesso.
- Testado na LG LJ600B (2017): ao vivo, filme e série tocaram.

## Riscos aceitos
- Dependência de app de terceiro: se o MSX mudar ou bloquear, o Sofae para nas TVs.
- Uso comercial ainda **não confirmado** pelo autor do MSX (e-mail redigido em 26/11).
- O cliente vê "Media Station X" na loja e precisa digitar `sofae.com.br` uma vez.
- Quem reinstala o MSX pode ganhar novo teste quando a TV não informa identificador fixo.

## Como funciona
Ver [[projetos/sofae]], seção "TV Samsung e LG pelo Media Station X".
