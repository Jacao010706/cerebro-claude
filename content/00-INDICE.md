# Índice

Porta de entrada do cofre. Comece por aqui.

## → [[projetos/sgm-trensurb]]

**O projeto principal.** Sistema dos geradores da Trensurb, usado pelo
SENERG. É onde o trabalho acontece.

## Outros projetos

- [[projetos/sgm-subestacoes]] — fase futura, 2590 ativos SAEE já importados
- [[projetos/simanplay-iptv]] — plataforma IPTV, projeto paralelo

## Sistemas e protocolos

- [[sistemas/modbus-stemac]] — ST2160: registradores, login, partida
- [[sistemas/modbus-dse]] — Gencomm: RPM, tensão, comando
- [[sistemas/estacoes-e-ips]] — códigos, IPs, controladores
- [[sistemas/supabase]] — tabelas, RLS, Realtime
- [[sistemas/railway]] — serviços, variáveis, deploy

## Armadilhas

Cada arquivo aqui representa horas já perdidas. Leia antes de propor
comandos.

- [[armadilhas/powershell-encoding]] — acentos corrompidos, colagem truncada
- [[armadilhas/deploy-railway]] — NEXT_PUBLIC, chave longa, build
- [[armadilhas/supabase-realtime]] — a chave precisa ser JWT

## Receitas de diagnóstico

- [[receitas/diagnostico-realtime]] — o WebSocket está conectando?
- [[receitas/diagnostico-backend]] — de onde vem esse 404?

## Decisões

- [[decisoes/2026-09-10-supabase]] — Supabase ao lado do Railway
- [[decisoes/2026-07-20-dois-sistemas]] — separar geradores de subestações

## Pendências abertas

### Segurança
- [ ] `JWT_SECRET` está com o valor literal `change_me_in_production`
- [ ] Rotacionar senha do Postgres, `admin2@sgm.com` e chave `sb_secret_`

### SGM Trensurb
- [ ] Descobrir por onde o coletor realmente reporta (não é `/api/iot/readings`)
- [ ] Service worker devolve corpo vazio em algumas rotas
- [ ] Instância duplicada do coletor deixa URL de túnel obsoleta no Redis
- [ ] Fases 2, 3 e 4 do Supabase (Storage, banco principal, Auth)

### OS e Inspeções
- [ ] Data de início e fim não gravam no banco
- [ ] Campo "referência do gerador" deve virar nome do local
- [ ] Falta gerar PDF das atividades de inspeção
- [ ] Periodicidade SEMANAL não existe como opção
- [ ] Agrupar inspeções por local e por data
- [ ] Listar só geradores que já têm inspeções

### Módulos ainda não mapeados
A tabela em [[projetos/sgm-trensurb]] lista 12 módulos que existem no
código mas nunca foram documentados aqui. Mapear conforme forem tocados.

## Diário

- [[diario/2026-09-10]] — Supabase Realtime em produção
