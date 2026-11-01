# Instruções para o Claude

Este é o cofre de conhecimento do Jacques. Você tem permissão para ler,
criar e atualizar qualquer arquivo aqui.

## Ao começar qualquer conversa sobre um projeto

1. Leia `00-INDICE.md` — ele diz o que existe e onde.
2. Leia a nota do projeto em `projetos/`.
3. Leia `armadilhas/` antes de propor comandos. Cada arquivo ali
   representa horas já perdidas; não repita.

Não peça ao Jacques para explicar a arquitetura. Está tudo escrito.
Se faltar algo, é porque ninguém registrou ainda — registre depois.

## Ao terminar qualquer trabalho

Atualize o cofre **antes** de encerrar. Especificamente:

- Descobriu um fato novo sobre a arquitetura → atualize a nota do sistema
  em `sistemas/`.
- Perdeu tempo com uma pegadinha → crie ou atualize um arquivo em
  `armadilhas/`. Escreva o **sintoma** primeiro, para ser encontrável.
- Tomou uma decisão de projeto → crie uma nota em `decisoes/` com a data
  no nome, explicando o **porquê**, não só o quê.
- Estabeleceu um procedimento de diagnóstico → `receitas/`.
- Resolveu ou abriu uma pendência → atualize `00-INDICE.md`.

## Regras de escrita

**Só registre o que foi verificado.** Se algo é suposição, marque como
`> DÚVIDA:` no texto. Muito tempo já se perdeu por hipótese plausível
tratada como fato.

**Escreva o sintoma, não só a causa.** Quem procura no futuro vai buscar
pelo que está vendo — "build falha com secret ID missing" — não pela
explicação.

**Prefira editar a criar.** Antes de fazer nota nova, procure uma
existente sobre o assunto.

**Nunca guarde segredos aqui.** Senhas, chaves, tokens: registre onde
encontrá-los (ex: "Railway → Variables"), nunca o valor.

## Como o Jacques quer receber alterações

Passo a passo numerado, com os comandos prontos para copiar, e sempre
explícito sobre onde cada um roda: **terminal PowerShell** ou **editor do
VS Code**. Nunca descreva a mudança esperando que ele posicione sozinho.
