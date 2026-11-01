# 2026-07-20 — Separar em dois sistemas

## Decisão

Criar dois sistemas separados no Railway: **SGM Geradores** (os ~25 GGDs
das estações) e **SGM Subestações** (as SEs com os 2590 ativos e 473
checklists). Unificar depois.

## Por quê

Os públicos e os ciclos de manutenção são diferentes. Manter tudo num
sistema só obrigava cada tela a filtrar por sistema, e as prioridades de
evolução competiam entre si.

## Estado

A decisão foi tomada mas **não executada** — os dois ainda vivem no mesmo
repositório. O painel CCO filtra por `sistema = "GGD's"`.
