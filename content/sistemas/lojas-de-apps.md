---
tags: [sofae, sistemas]
---

# Lojas de apps — contas e estado

## Google Play

- Conta de desenvolvedor **Akitemtech** (conta pessoal, sem CNPJ).
  ID da conta: ver Play Console. App **Sofae** (`com.sofae.app`).
- Teste fechado iniciado em 24/10 (faixa **Alpha**); **acesso de produção
  concedido** em nov/2026.
- 18/11: enviado para revisão — produção **1003 (1.1.0)** para o **Brasil**,
  teste fechado também trocado para a 1003, ficha nova, política nova,
  Segurança dos dados refeita, "Detalhes do login: Não".
- Pendente: declarar **status de comerciante** até fev/2027.
- Caminhos no console novo:
  - Versões: foguete → Testar e lançar → Produção
  - Ficha: Aumentar número de usuários → Páginas de detalhes do app → Editar página padrão
  - Conteúdo do app: `.../app/<id>/app-content/overview`
  - Envio: Visão geral da publicação → "Enviar N mudanças para revisão"

## Amazon Appstore

- **Conta certa:** `jacquessiman@yahoo.com.br` (aparece como "J"; o Jacques
  usa pelo **Edge**). É Administrador e o Sofae está nela.
- `akitemtech@gmail.com` é **outra** conta de desenvolvedor: vazia, nome
  legal "aki", verificação de identidade falhada. Não usar.
- `jacao010706@gmail.com`: cadastro de desenvolvedor começado em 17/11 e
  **não terminado** (não terminar — evita conta duplicada).
- 14/11: APK 147 **recusado** por cobrança sem IAP (PIX/QR/links) e por
  criar conta e cobrar uso.
- 17/11: enviado o **1003** (Fire TV 93 modelos + Fire Tablet 12, sem
  Automotive), DRM: No, Free, ficha/capturas/promocional novas, nota para o
  revisor, questionário de privacidade só com "User IDs".

## Textos e imagens prontos (17/11)

- Capturas 1920×1080: `sofae-1-login`, `sofae-2-inicio`, `sofae-3-filmes`,
  `sofae-4-ao-vivo` (telas reais da versão de loja, modo demonstração).
- Imagem promocional / recurso gráfico 1024×500: `sofae-promo-1024x500`.
- Descrição: "player para a sua própria lista (Xtream Codes ou M3U)…
  o Sofae não fornece, não vende e não hospeda conteúdo". Nunca citar
  canais, campeonatos, marcas de TV, preço ou "assinatura".
- Política de privacidade (pública): artifact
  `claude.ai/artifact/4Zmm4rwbjPpC6gNup5BVs6` — inclui Xtream e M3U, modo
  demonstração e a seção "Como excluir seus dados" (usada também como link
  de exclusão de dados na Play).

## Outras lojas (de antes)

LG Content Store (Sofae 1.1.0 em QA desde 19/10), Samsung TV Seller Office,
Galaxy Store, Roku — ver [[simanplay-iptv]].

## Ver também

[[armadilhas/lojas-recusam-cobranca]] · [[decisoes/2026-11-16-sofae-lojas-gratuito]]
