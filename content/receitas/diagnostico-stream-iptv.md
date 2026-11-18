---
tags: [sofae, receitas]
---

# Canal / filme não toca — é o app ou é a lista?

Ordem que resolveu os casos de 13 a 16/11:

1. **Outro player, mesma lista, mesma rede.** Se o outro toca e o Sofae
   não, é o app. Se nenhum toca, é a lista/provedor/rede.
2. **Conta com 1 conexão** (`max_connections: 1`): fechar de verdade o
   outro app (Configurações → Apps → Forçar parada), esperar 2 min.
   `active_cons` no `player_api.php` mostra se a linha está ocupada.
3. **Rede de casa alcança o provedor?** Abrir `http://<servidor>` no
   navegador do PC. `ERR_CONNECTION_TIMED_OUT` = a internet não chega lá
   (aconteceu com o provedor de teste). Testar pelo 4G/roteador do celular.
4. **Erro `_Map<String, dynamic> is not a subtype of List<dynamic>`**: o
   servidor respondeu um objeto (normalmente `user_info.auth: 0` — conta
   recusada naquele momento) em vez da lista. Nas versões novas isso já
   vira mensagem clara.
5. **Excesso de chamadas** pode bloquear a conta por um tempo. Não ficar
   testando a mesma conta de vários IPs (VPS, Vercel, casa, 4G) no mesmo dia.
6. **Mostrar a versão** do app antes de testar (Home: "Sofae v1.0.0+N";
   no Windows: botão direito no `.exe` → Propriedades → Detalhes).

Pôr o erro real na tela antes de teorizar — mesma lição de
[[diario/2026-09-10]].
