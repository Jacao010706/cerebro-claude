---
tags: [simanplay]
cor: "#2ecc71"
emoji: 🟢
tipo: projeto
status: ativo
---

# 🟢 SimanPlay IPTV

Plataforma white-label de gestão de IPTV. Projeto paralelo, construído do
zero a partir de jun/2026.

## Peças

| Peça | Onde | Nota |
|---|---|---|
| App Flutter | `Jacao010706/simanplay-iptv-app` | APK por marca via GitHub Actions |
| Backend FastAPI | Railway, projeto "siman play iptv", serviço `web` | [[simanplay-iptv-backend]] |
| Painel Next.js | Vercel | [[simanplay-iptv-admin-panel]] |
| Banco | PostgreSQL no Railway | — |
| Bot WhatsApp | VPS | [[simanplay-iptv-whatsapp]] |
| Marca própria de loja | — | [[sofae]] |

## Modelo de negócio (decidido em out/2026)

App grátis + teste de 7 dias + assinatura paga **fora das lojas** (PIX,
pelo painel). Revendedores com hierarquia e créditos (1 crédito = 1 mês).
Os revendedores atuais (PRIMETV, Martins, Sofae) são todos do próprio
Jacques; nenhum cliente externo ainda (out/2026).

> Em nov/2026 as lojas recusaram cobrança fora do sistema delas. Nas lojas
> o Sofae virou grátis e só player: [[decisoes/2026-11-16-sofae-lojas-gratuito]].

## Como o APK de cada marca é gerado

- Workflow `build_apk.yml`, disparado só por `workflow_dispatch` (o backend
  chama com os dados da marca salvos no painel).
- A marca não usa flavor: o workflow troca as constantes de
  `lib/core/app_config.dart` com `sed` (nome, cores, tema, logo, banner,
  buildNumber, revendedor) e gera ícone/banner com Pillow.
- Release por marca com tag `apk-<revendedor>-<N>` (Sofae: `apk-sofae-147`).
- `auto_rebuild.yml` só dispara em push na `main`.
- Assinatura: secrets `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`.
- A pasta `windows/` existe desde 02/10, mas só foi compilada no CI em
  14/11 (branch `sofae-windows`).

## Arquitetura do app (pontos que importam)

- Tela de login ativa: `activation_screen_v3.dart`.
- Player: media_kit (libmpv). Funciona em Android, Fire TV e Windows.
- URLs: `$host/live/u/s/ID.m3u8`, `/movie/u/s/ID.ext`, `/series/u/s/ID.ext`
  — direto ao servidor do cliente, **sem proxy**.
- "Fonte 1/2, 2/2" = `.m3u8` e depois `.ts`.
- 6 temas visuais; o tema 6 é o favorito (banner IBO + navegação inferior).
- Aba Jogos: backend `/sports/fixtures` (API-Football) + cruzamento com os
  canais de esporte e a grade. Ver [[sistemas/apifootball-relay]].

## Lojas de TV (out/2026)

LG Content Store (Sofae 1.1.0 em QA desde 19/10), Samsung TV Seller Office,
Galaxy Store, Roku (canal grátis). Fire TV Stick com **Vega OS** não aceita
APK por fora — só loja. Ver [[sistemas/lojas-de-apps]].

## Pendências conhecidas (antes de nov/2026)

- [ ] Acentos quebrados nos cabeçalhos da tabela de revendedores
- [ ] Integração DNA-GO: endpoint não encontrado
- [ ] Melhorias da branch `sofae-windows` ainda não estão na `main`
