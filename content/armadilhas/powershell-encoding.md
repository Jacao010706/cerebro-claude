# PowerShell corrompe acentos

## Sintoma

Depois de rodar um comando que lê e grava um arquivo, os acentos viram
lixo: `SUPERVISÓRIO` aparece como `SUPERVISÃ"RIO`, `TRENSURB —` vira
`TRENSURB â€"`.

## Causa

`Get-Content -Raw` sem `-Encoding` lê arquivo UTF-8 **sem BOM** como
ANSI. Gravar de volta destrói os acentos.

## Solução

Sempre .NET com codificação explícita:

```powershell
$txt = [System.IO.File]::ReadAllText($f, [System.Text.Encoding]::UTF8)
# ... modificar ...
[System.IO.File]::WriteAllText($f, $txt, (New-Object System.Text.UTF8Encoding($false)))
```

## Ao detectar mojibake, cuidado

Procure `â€`, `Ã©`, `Ã§`, `Ã£`, `Ã³`.

**Não** procure `Ã` sozinho — é letra legítima do português, como em
`SÃO LEOPOLDO`. Esse detector errado já gerou um falso alarme e meia
hora de investigação desnecessária.

## Relacionado: o terminal do VS Code trunca colagens

Acima de cerca de 700 caracteres a colagem é cortada no meio, sem aviso —
o PowerShell fica esperando com `>>` porque a aspa nunca fechou.

Para conteúdo grande: cole no **editor**, salve como arquivo, execute o
arquivo.
