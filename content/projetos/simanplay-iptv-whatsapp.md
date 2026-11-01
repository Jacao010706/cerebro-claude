---
title: SimanPlay IPTV WhatsApp Bot
tags: [simanplay]
---

# SimanPlay IPTV WhatsApp Bot

Bot de atendimento automático para clientes do [[simanplay-iptv]] via WhatsApp.

## Stack
- whatsapp-web.js (automação WhatsApp Web)
- Node.js + TypeScript
- Supabase (PostgreSQL) — base de conhecimento e histórico
- Claude API (fallback de respostas)
- pm2 (processo persistente na VPS)

## VPS
- Host: ubuntu-4gb-nbg1-1 (Hetzner CX23)
- Pasta: /root/simanplay-iptv-whatsapp
