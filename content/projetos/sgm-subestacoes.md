# SGM Subestações — fase futura

Não é o projeto em que estamos trabalhando. O foco atual é
[[projetos/sgm-trensurb]], que cobre só os geradores.

## O que já existe

- **2590 ativos SAEE** importados de `PLANO SAEE OFICIAL.xlsx` em
  18/07/2026, em 26 lotes de INSERT
- **473 templates de checklist** e 4034 itens importados em 20/07/2026
  — 138 kV, 3 kVcc, 6,6 kVca, 69 kVca, auxiliares, CP MR, CSP AN, CSP CN
- Módulo SAEE deployado em 19/07/2026

## Campos de `saee_ativos`

`local` · `sublocal` · `sistema` · `nome_ativo` · `tag` · `esp_tecnica` ·
`tag_diagrama` · `diagrama` · `item_contrato` · `periodicidade` · `area` ·
`data_ult_manu` · `proxima_manu`

O painel CCO filtra por `sistema = "GGD's"` para pegar só os geradores —
por isso os dois convivem hoje na mesma tabela.

## Pendente

A separação em dois sistemas foi decidida em julho mas não executada.
Ver [[decisoes/2026-07-20-dois-sistemas]].
