---
tags: [sofae, armadilhas]
---

# Canal ao vivo não abre no navegador (401/403 no proxy)

## Sintoma

No web app, canal ao vivo fica em "Carregando..." para sempre. No DevTools:
`/api/proxy?url=http://<provedor>/live/...m3u8` volta 200, mas os
segmentos (`/hls/...`) voltam **403**; ou o proxy do VPS volta **401** já
na playlist. Filmes e séries tocam normal. **No app nativo, o mesmo canal toca.**

## Causa (verificada em 14/11 com o provedor de teste)

O provedor libera a API (`player_api.php`) para qualquer IP, mas recusa o
**endpoint de stream** para IPs de datacenter — mesmo brasileiros:

| Origem | Stream |
|---|---|
| VPS Hetzner (Alemanha) | 401 |
| Vercel fra1 | 401 |
| Vercel gru1 / AWS São Paulo (IP fixo) | 401 |
| Navegador → Vercel (São Paulo) | playlist 200, segmentos 403 |

O navegador é obrigado a usar proxy porque a página é `https://` e o stream
é `http://` (conteúdo misto). App nativo não tem esse problema: conecta
direto com o IP da casa do cliente.

> DÚVIDA: o "200 na playlist via Vercel" pelo navegador nunca foi explicado
> por completo. A hipótese de repassar `X-Forwarded-For` com o IP do cliente
> foi **descartada de propósito** — ver [[decisoes/2026-11-14-nao-burlar-bloqueio-iptv]].

## O que fazer

- Não gastar mais tempo com proxy, região da Vercel ou VPS no Brasil.
- Canal ao vivo é no **app** (Android, Fire TV, Windows). A web mostra
  mensagem + botão de baixar o app.
- Antes de culpar o app, testar a mesma lista em outro player/VLC na
  mesma rede. Ver [[receitas/diagnostico-stream-iptv]].
