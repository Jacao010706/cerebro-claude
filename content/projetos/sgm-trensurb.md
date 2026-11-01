---
tags: [sgm]
tipo: projeto
status: ativo
---

# SGM Trensurb

**O projeto principal.** Sistema de gestão de manutenção dos grupos
geradores diesel das estações da Trensurb, usado pelo SENERG.

Escopo atual: **apenas os geradores**. As subestações são fase futura —
ver [[projetos/sgm-subestacoes]].

## Os três nomes do mesmo projeto

Isso confunde quem chega. É tudo a mesma coisa:

| Onde | Nome |
|---|---|
| Repositório local | `sgm-trensurb` |
| `package.json` | `sgm-geradores` |
| Serviço no Railway | `sgm-geradores-trensurb` |
| Cabeçalho do painel | TRENSURB — SENERG · SUPERVISÓRIO CCO · GERADORES |

Chame de **SGM Trensurb**.

## Por que existe

Falta de histórico de manutenção dos equipamentos e registros de
preventiva sem detalhe suficiente. O painel é meio, não fim.

## Onde vive

| Peça | Endereço |
|---|---|
| Produção | `sgm-geradores-trensurb-production.up.railway.app` |
| Backend FastAPI | `laudable-peace-production-09cd.up.railway.app` |
| Repo local (casa) | `C:\Users\Jacques\Downloads\sgm-trensurb` |
| Repo local (Trensurb) | `C:\Users\jacques.siman\sgm-geradores-trensurb` |
| Coletor | PC E011011, IP 10.3.10.45, rede Trensurb |
| Banco | Postgres no Railway · Supabase em adoção |

## Módulos do sistema

O que existe em `src/app/`. As marcações dizem o que já foi mapeado neste
cofre e o que ainda não.

| Módulo | Rota | Estado no cofre |
|---|---|---|
| Painel CCO | `/cco` | ✅ mapeado — ver abaixo |
| Leituras IoT | `/api/iot/readings` · `/api/iot/command` | ✅ mapeado |
| Ordens de serviço | `/os` | ⬜ não mapeado |
| Inspeções | `/inspecoes` | ⬜ não mapeado |
| Preventivas | `/preventivas` | ⬜ não mapeado |
| Relatórios | `/relatorios` | ⬜ não mapeado |
| Estoque | `/estoque` | ⬜ não mapeado |
| Usuários e times | `/usuarios` · `/teams` | ⬜ não mapeado |
| Contratos e equipamentos | `/contratos` · `/equipamentos` | ⬜ não mapeado |
| APR / Permissão de trabalho | `/apr` · `/apr-templates` | ⬜ não mapeado |
| Checklists | `/checklist-templates` · `/checklist-execucoes` | ⬜ não mapeado |
| KPIs e dashboard | `/kpis` · `/dashboard` | ⬜ não mapeado |
| Notificações push | `/push` · `/notificacoes` | ⬜ não mapeado |
| App SGM Técnico | React Native / Expo, pasta `mobile/` | ⬜ não mapeado |

> Mapear um módulo significa: abrir o código, entender o fluxo real, e
> escrever aqui o que foi **verificado** — não o que parece ser.

## Painel CCO — o que foi verificado

`src/app/cco/page.tsx`, cerca de 860 linhas.

### Quem olha

Uma tela fixa no CCO e outra na sala dos técnicos, ligadas o tempo todo,
mais chefe, gestor, supervisores e admin.

**Consequência de projeto:** o painel não pode mostrar tela de erro. As
telas fixas não têm ninguém para recarregá-las. Toda integração nova
degrada em silêncio ou não entra.

### Fluxo do dado

```
coletor_modbus.py  →  POST /api/iot/readings  →  iot_readings + Map
                                                       ↓
                          painel /cco  ←  GET, ~22 chamadas / 30 s
```

É **push**, não pull. As chamadas do painel não tocam o Modbus.

> DÚVIDA: os logs do Supabase provaram que o coletor **não** usa
> `POST /api/iot/readings`. Achar a URL real no `coletor_modbus.py`.

### Estado

- `ativos: Ativo[]` ← `/api/v1/saee-ativos?sistema=GGD's`
- `iotData: Record<sublocal, IotEntry>` ← `/api/iot/readings`
- `IotEntry = { readings: Record<string, number>, status_com, timestamp }`

**Atenção aos acentos:** chaves de `iotData` têm acento (`RODOVIÁRIA`),
banco guarda sem (`RODOVIARIA`). Normalize os dois lados ou nunca casa.

### Cores do card

| Cor | Significa |
|---|---|
| Vermelho | Rodando |
| Amarelo | Sem comunicação há mais de 10 min |
| Azul | Parado |

Telemetria só vale se tiver menos de 5 minutos. "0 ONLINE" com o coletor
desligado é correto, não defeito.

### Acesso

Painel público, sem login. Protegido apenas pelo whitelist do middleware
com a senha de admin.

## Ver também

[[sistemas/supabase]] · [[sistemas/modbus-stemac]] · [[sistemas/railway]] ·
[[armadilhas/deploy-railway]] · [[receitas/diagnostico-realtime]]
