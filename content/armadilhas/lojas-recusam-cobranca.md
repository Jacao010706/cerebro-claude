---
tags: [sofae, armadilhas]
---

# Loja recusa o app (cobrança, dados, revisor)

## Amazon: "Not compliant" — Monetization Policy

### Sintoma
App Status → Details: "Your app makes digital content available for
purchase… without using Amazon IAP" e "enables account creation… and
charges end users".

### Causa
O APK do painel tem PIX, QR de pagamento, preços, link do site e licença
com teste de 7 dias. Amazon e Google proíbem cobrar conteúdo digital fora
do sistema deles — **até mostrar link ou QR** que leve a pagar fora conta.

### Solução
Versão de loja **gratuita, só player** (branch `sofae-loja`). Ver
[[decisoes/2026-11-16-sofae-lojas-gratuito]].

## Google Play: "Declaração de segurança dos dados inválida"

### Sintoma
Ao enviar: "1 problema foi encontrado… Identificadores do dispositivo e
outros IDs — Código da versão: 1".

### Causa
A declaração vale para **todas as faixas ativas**. A faixa de teste
fechado ainda tinha a versão 1 (com MAC/ID do aparelho). A declaração nova
(sem ID do aparelho) "mentia" sobre ela.

### Solução
Trocar o pacote da faixa de teste fechado pela versão nova
("Adicionar da biblioteca" — subir o mesmo `.aab` de novo dá
"código de versão já usado"). Conferir que a versão antiga ficou em
"Não incluídos".

## Questionário de dados vindo do app antigo

Ao refazer a Segurança dos dados / Privacy Questionnaire, desmarcar o que
era do app antigo: **Local aproximado**, **Interações no app** ("assistindo
agora"), **ID do dispositivo**, e o login externo ("assinatura de serviço").
Criptografia em trânsito: **Não** (listas IPTV costumam ser `http`).

## Detalhes do login com lista IPTV real

Não deixar credencial de lista IPTV real para o revisor: ele veria canais
pagos. Marcar "nenhuma parte é restrita" e apontar o modo demonstração.

## Amazon: dispositivos

O release novo veio com **1** Fire TV marcado. Editar e marcar todos; tirar
**Automotive** (vídeo em carro). Release notes é **obrigatório**.
