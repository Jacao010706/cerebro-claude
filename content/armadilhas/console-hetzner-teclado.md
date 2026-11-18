---
tags: [infra, armadilhas]
---

# Console web da Hetzner quebra comandos colados

## Sintoma

Comando colado no console da Hetzner sai diferente do que foi copiado:
- `cd /pasta && vercel --prod` → `bash: cd: too many arguments`
- `curl http://localhost:3002/health` → `Could not resolve host: http` e
  `2/localhost:3002/health: No such file or directory`
- `grep ... | head` → o `|` vira `\` (`grep: head: No such file or directory`)
- `play(` vira `play9`
- Ctrl+V não cola nada.

## Causa

O console é VNC e envia **teclas**, não texto. Com o teclado ABNT2, os
caracteres com Shift chegam trocados: `( ) | : " & ? *`.

## Solução

1. **Usar VS Code Remote-SSH** (`vps-hetzner`). Resolve tudo.
2. Se só tiver o console: um comando por linha, **sem** `&&`, `|`, `://`,
   parênteses ou aspas duplas. Ex.: `wget -O- localhost:3002/health`
   em vez de `curl http://...`.
3. Cuidado: um comando mal colado criou um arquivo-lixo
   `ystemctl status sofae-proxysystemctl...` dentro de `/root/sofae-webapp`,
   que teria ido no deploy. Conferir a pasta antes de `vercel --prod`.
