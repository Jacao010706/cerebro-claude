---
tags: [infra, armadilhas]
---

# Claude Code diz "Credit balance too low"

## Sintoma

O Claude Code (no VPS ou no PC) para no meio com
`Credit balance too low · Add funds`, mesmo com a assinatura do Claude ativa.
Depois de `/login` com "Claude.ai Subscription", aparece um aviso amarelo
sobre `ANTHROPIC_API_KEY`.

## Causa

Existe uma variável `ANTHROPIC_API_KEY` (chave de API sem crédito) no
ambiente, e ela tem prioridade sobre o login da assinatura. No VPS ela
estava em `~/.bashrc`, linhas 100–101 (a chave quebrada em duas linhas).

## Solução (VPS, 14/11)

1. `cp ~/.bashrc ~/.bashrc.bak`
2. `sed -i '100,101s/^/# /' ~/.bashrc` (comentar as linhas, não apagar)
3. `bash -n ~/.bashrc` (sem saída = arquivo válido)
4. VS Code: Ctrl+Shift+P → **Kill VS Code Server on Host** → Reload Window.
5. Claude Code → `/login` → **Claude.ai Subscription**.

Nunca colar a chave em chat: para ver as linhas, mostrar só o começo
(`awk 'NR>=98 && NR<=104 {print NR": "substr($0,1,14)"..."}' ~/.bashrc`).
