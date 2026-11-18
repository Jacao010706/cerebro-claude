# Índice

Porta de entrada do cofre. Comece por aqui.

## → [[projetos/sgm-trensurb]]

**O projeto principal.** Sistema dos geradores da Trensurb, usado pelo
SENERG. É onde o trabalho acontece.

## Outros projetos

- [[projetos/sgm-subestacoes]] — fase futura, 2590 ativos SAEE já importados
- [[projetos/simanplay-iptv]] — plataforma IPTV, projeto paralelo
- [[projetos/sofae]] — marca própria: loja (Play/Amazon), Windows e web

## Sistemas e protocolos

- [[sistemas/modbus-stemac]] — ST2160: registradores, login, partida
- [[sistemas/modbus-dse]] — Gencomm: RPM, tensão, comando
- [[sistemas/estacoes-e-ips]] — códigos, IPs, controladores
- [[sistemas/supabase]] — tabelas, RLS, Realtime
- [[sistemas/railway]] — serviços, variáveis, deploy
- [[sistemas/vps-hetzner]] — o que roda no VPS, Caddy, memória, acesso
- [[sistemas/sofae-proxy]] — proxy de streams do web app
- [[sistemas/apifootball-relay]] — aba Jogos pelo IP do VPS
- [[sistemas/lojas-de-apps]] — contas Google Play / Amazon e estado

## Armadilhas

Cada arquivo aqui representa horas já perdidas. Leia antes de propor
comandos.

- [[armadilhas/powershell-encoding]] — acentos corrompidos, colagem truncada
- [[armadilhas/deploy-railway]] — NEXT_PUBLIC, chave longa, build
- [[armadilhas/supabase-realtime]] — a chave precisa ser JWT
- [[armadilhas/iptv-bloqueia-datacenter]] — canal ao vivo não abre no navegador
- [[armadilhas/console-hetzner-teclado]] — comando colado sai trocado
- [[armadilhas/service-worker-cache]] — deploy da web não muda nada
- [[armadilhas/claude-code-api-key]] — "Credit balance too low"
- [[armadilhas/lojas-recusam-cobranca]] — Amazon/Play recusam o app
- [[armadilhas/m3u-mistura-vod]] — pastas de filmes no Ao Vivo

## Receitas de diagnóstico

- [[receitas/diagnostico-realtime]] — o WebSocket está conectando?
- [[receitas/diagnostico-backend]] — de onde vem esse 404?
- [[receitas/diagnostico-stream-iptv]] — é o app ou é a lista?

## Decisões

- [[decisoes/2026-09-10-supabase]] — Supabase ao lado do Railway
- [[decisoes/2026-07-20-dois-sistemas]] — separar geradores de subestações
- [[decisoes/2026-11-14-nao-burlar-bloqueio-iptv]] — web não toca ao vivo; app nativo
- [[decisoes/2026-11-15-jogos-plano-b]] — jogos a partir da lista, sem pagar
- [[decisoes/2026-11-16-sofae-lojas-gratuito]] — Sofae nas lojas grátis, só player
- [[decisoes/2026-11-16-apifootball-via-vps]] — API-Football pelo IP do VPS

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

### Sofae / SimanPlay (nov/2026)
- [ ] Revisão Google Play (enviado 18/11) e Amazon (enviado 17/11)
- [ ] API-Football suspensa — falar com atendente humano (seg–sex 4h–13h)
- [ ] Trocar o botão "Baixar o app" da web pelos links das lojas
- [ ] Microsoft Store para o Sofae Windows
- [ ] Status de comerciante no Play Console (até fev/2027)
- [ ] Apagar o repositório público `sofae-tmp`
- [ ] Levar as melhorias da `sofae-windows` para a `main`

### Módulos ainda não mapeados
A tabela em [[projetos/sgm-trensurb]] lista 12 módulos que existem no
código mas nunca foram documentados aqui. Mapear conforme forem tocados.

## Diário

- [[diario/2026-09-10]] — Supabase Realtime em produção
- [[diario/2026-11-13]] — proxy de streams no VPS
- [[diario/2026-11-14]] — bloqueio de datacenter; nasce o Sofae Windows
- [[diario/2026-11-15]] — Windows tocando; Ao Vivo só canais; produção na Play
- [[diario/2026-11-16]] — plano B dos jogos; relay API-Football; branch sofae-loja
- [[diario/2026-11-17]] — Amazon: 1003 enviado
- [[diario/2026-11-18]] — Google Play: enviado para revisão
