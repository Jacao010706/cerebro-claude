---
tags: [simanplay, decisoes]
---

# 2026-11-15 — Aba Jogos sem pagar API

## Decisão

Não pagar a API-Football por enquanto. Quando o backend falhar, o app monta
os jogos a partir da **própria lista do cliente**, sem placar. Feito só no
app (branch `sofae-windows`), sem mexer no backend.

## Por quê

- O Jacques preferiu não ter o custo (~US$ 19/mês) agora.
- Mexer no backend arrisca todas as marcas de uma vez.

## Como ficou

- Fontes: canais com data/hora no nome em categorias JOGOS/PPV/EVENTOS e a
  grade (`xmltv.php`, 1 download de ~9 MB; complemento canal a canal em no
  máximo 25 canais, 2 por vez) dos canais de esporte.
- Descarta reprise ("VT", "REPRISE", "JOGO COMPLETO", "MELHORES MOMENTOS"…).
  Regra "AO VIVO" adaptável: se o painel marca 3+ jogos "Ao Vivo" no dia,
  exige a marca; se não marca, aceita 08:00–23:59 sem o mesmo confronto nas 48 h.
- "Hoje a partir das 20:30 – X x Y" vira jogo às 20:30.
- Escudos via TheSportsDB (cache em disco 7 dias); na dúvida, iniciais.
- Cópia em disco por dia (até 3 dias) — é o que mantém "Ontem".
- Para em conta recusada (auth 0/401/403/429).
- Pedidos ao painel: 3 na primeira abertura, 0 nas trocas de dia.

## Depois

Em 16/11 o placar voltou a ser possível sem pagar: ver
[[decisoes/2026-11-16-apifootball-via-vps]]. O plano B fica como reserva.
Na versão de **loja** a aba Jogos não existe.
