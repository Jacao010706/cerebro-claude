# Deploy no Railway — três armadilhas

## 1. `NEXT_PUBLIC_*` é embutida no BUILD

### Sintoma
Você muda o valor no Railway, o deploy diz sucesso, e o navegador
continua com o comportamento antigo.

### Causa
Variáveis `NEXT_PUBLIC_` são embutidas no JavaScript **durante o build**.
Mudar o valor e clicar em **Redeploy** reinicia o serviço mas nem sempre
reconstrói.

### Solução
```powershell
git commit --allow-empty -m "chore: forca rebuild"
git push
```
Um push sempre reconstrói.

## 2. Colar chave longa quebra o build

### Sintoma
```
failed to solve: secret ID missing for "" environment variable
```

### Causa
Uma quebra de linha invisível no valor colado gera uma variável de
**nome vazio**.

### Solução
Cole primeiro no Bloco de Notas, confirme que é uma linha só sem espaço
no fim, e só então leve para o Railway. Ou prefira valores curtos.

## 3. `tsc --noEmit` não é igual a `npm run build`

### Sintoma
Passa local, quebra no Railway com `Type error`.

### Causa
O build de produção roda com `noImplicitAny`. O modo dev e o
`tsc --noEmit` aceitam o que ele recusa.

### Solução
Valide sempre com `npm run build` antes do push.
