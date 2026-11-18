---
tags: [sofae, armadilhas]
---

# Deploy da web não muda nada (service worker)

## Sintoma

Fez `vercel --prod`, o arquivo novo está no servidor, mas o navegador
continua rodando o JS antigo — mesmo em aba anônima recém-aberta às vezes.

## Causa

O `sw.js` do web app do [[sofae]] guarda os arquivos em cache. Sem mudar a
versão do cache, o navegador continua servindo o antigo.

## Solução

1. A cada deploy de JS/CSS: subir a versão no `sw.js`
   (`sofae-v7` → `sofae-v8` → …).
2. Para testar: fechar **todas** as abas anônimas e abrir uma nova.
3. Para confirmar o que está em produção, baixar o arquivo do servidor
   (não confiar no que o navegador mostra).
4. Não esquecer de ignorar `*.bak` no `.vercelignore` — o primeiro deploy
   de 14/11 publicou os backups.

## Pendente

O `sw.js` grava qualquer página do domínio no lugar do `/index.html`
(linhas 41–50). Abrir o `windows-version.json` numa aba e depois usar o app
offline mostra o JSON. Correção: só guardar respostas HTML.
