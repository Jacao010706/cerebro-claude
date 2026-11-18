---
tags: [simanplay, decisoes]
---

# 2026-11-16 — API-Football pelo IP do VPS

## Decisão

Fazer o backend chamar a API-Football através de um repasse no VPS (IP
exclusivo), em vez de pagar o plano Pro ou o Railway Pro.

## Opções avaliadas

| Opção | Custo | Problema |
|---|---|---|
| API-Football Pro | ~US$ 19/mês | — (simples, mas o Jacques não quis pagar) |
| Railway Pro com IP fixo | US$ 20/mês | o IP fixo do Railway **pode ser compartilhado** |
| Repasse no VPS | grátis | mexe no backend |

O suporte da API-Football confirmou que IP dedicado permite reativar a
conta grátis.

## Como foi feito com risco baixo

- Autorização limitada: só `sports.py` no backend.
- Sem as variáveis novas, comportamento idêntico ao anterior.
- O push foi sem o pytest (o VPS não tinha `ensurepip`): o diff só mudava
  URL e header, compilava, e a única rota afetada já estava quebrada.

Detalhes: [[sistemas/apifootball-relay]].
