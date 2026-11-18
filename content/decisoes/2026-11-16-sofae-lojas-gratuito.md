# 2026-11-16 — Sofae nas lojas: grátis, só player

## Decisão

Na Google Play e na Amazon, o Sofae é **gratuito e só player**: sem
licença, sem teste de 7 dias, sem PIX/QR/preço, sem MAC, sem atualizador,
sem aba Jogos. Branch `sofae-loja`, separada de tudo que já existe.

## Por quê

- Amazon recusou o APK 147 por cobrança fora do IAP.
- Google tem a mesma regra (faturamento do Google Play obrigatório para
  conteúdo digital; não pode levar a pagar fora). Para o Brasil, as regras
  de pagamento alternativo ainda não estavam claras em nov/2026.
- Opções avaliadas: (A) grátis nas lojas; (B) assinatura pelo faturamento da
  loja (mais trabalho + taxa); (C) só código de ativação (arriscado).
  Escolhida a **A**. A B pode ser estudada depois.

## O que não muda

APK direto do painel, outras marcas, backend, painel, web, Windows.
Quem usa o APK do painel continua igual. O faturamento fica fora das lojas.

## Ids

As lojas ficam com `com.sofae.app` — esse id já tinha **acesso de produção**
na Play (12 testadores × 14 dias). Trocar perderia isso.
O APK direto usa o **mesmo id** hoje: quem tem um instalado não instala o
outro por cima (assinaturas diferentes). Trocar o id do APK direto exige
mudar o painel/backend (o id do revendedor fica travado depois do primeiro
APK) e ajustar `ModoTv.sofaeTv` → fica para depois, com autorização.
