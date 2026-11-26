---
tags: [indice]
---

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
- [[armadilhas/lojas-recusam-cobranca]] — Amazon/Play recusam o app (cobrança, "Fire TV", capturas)
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
- [[decisoes/2026-11-25-sofae-tv-via-msx]] — Sofae nas TVs Samsung/LG pelo Media Station X

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
- [x] Google Play: Sofae publicado (celular); status de comerciante declarado
- [ ] Google Play: revisão do Android TV + AAB 1009; depois enviar o AAB 1011 e trocar o quadro Android TV do site
- [x] Amazon Appstore: versão 1011 no ar (25/11) — https://www.amazon.com/dp/B0HRJ7X68T
- [x] TVs Samsung e LG pelo Media Station X (26/11) — ver [[decisoes/2026-11-25-sofae-tv-via-msx]]
- [ ] LG Content Store: Sofae 1.1.0 em QA desde 19/10; pergunta aberta no 1:1 Q&A em 26/11 (conta de teste `lgteste` vence 05/01/2027)
- [ ] Media Station X: enviar o e-mail ao autor e registrar a resposta sobre uso comercial
- [ ] Vega OS parado: instalar Ubuntu no HD externo de 500 GB do outro PC para rodar o simulador
- [ ] Separar login de admin e de revendedor no mesmo navegador
- [ ] Vídeos dos tutoriais do site
- [x] API-Football: conta nova ativa, aba Jogos funcionando (19/11)
- [ ] Trocar o botão "Baixar o app" da web pelos links das lojas
- [ ] Microsoft Store para o Sofae Windows
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
- [[diario/2026-11-19]] — aba Jogos voltou (conta nova da API-Football)
- [[diario/2026-11-20]] — Amazon: categoria e layout de TV corrigidos, reenviado
- [[diario/2026-11-21]] — Android TV na Play, banner WhatsApp, Vega fase 1
- [[diario/2026-11-26]] — Sofae nas TVs Samsung/LG (Media Station X), Amazon 1011 no ar
