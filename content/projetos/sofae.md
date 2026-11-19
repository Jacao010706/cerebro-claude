---
tags: [sofae, projetos, simanplay]
cor: "#FF8A1A"
emoji: 🛋️
tipo: projeto
status: ativo
---

# 🛋️ Sofae

Player de IPTV com a marca própria do Jacques. Nasceu como marca
white-label do [[simanplay-iptv]] e virou produto de loja.

- Domínio: `sofae.com.br` (Registro.br). E-mail da marca: ver Gmail `sofaeapp.tv`.
- Pacote Android: `com.sofae.app`
- Visual: laranja `#FF8A1A`, fundo `#1A0B33`, superfície `#2E1F4D`, tema 6.
- Contato público nas lojas e na política: `akitemtech@gmail.com`.

## As quatro versões do Sofae (nov/2026)

| Versão | Onde está o código | Para quem | Estado |
|---|---|---|---|
| **APK direto (painel)** | `main` do `simanplay-iptv-app`, gerado pelo `build_apk.yml` (tag `apk-sofae-N`) | clientes de revendedor, com licença/MAC/PIX | intocado |
| **Loja (Play + Amazon)** | branch `sofae-loja` | público geral, **grátis, só player** | em revisão nas duas lojas |
| **Windows + APK de teste** | branch `sofae-windows` | testes no PC | funcionando |
| **Web** | `/root/sofae-webapp` → Vercel (`app.sofae.com.br`) | navegador | filmes/séries ok, ao vivo manda para o app |

Regra que valeu o mês inteiro: **nada na `main`, nos workflows existentes,
nem no painel/backend** sem autorização explícita. Tudo em branch própria.

## Versão de loja (`sofae-loja`)

- Base: `feature/sofae-release` + merge da `sofae-windows`.
- Tudo atrás de `Loja.play` (constante): o APK do painel não muda.
- **Removido na loja:** LicenseGate, teste grátis, bloqueio por tempo, tela do
  aparelho (MAC/chave/QR), "assistindo agora", atualizador de APK,
  `REQUEST_INSTALL_PACKAGES`, aba **Jogos** (canais pagos = risco de recusa).
- Abre direto em **Xtream / URL M3U** + botão **"Ver demonstração (filmes
  livres, sem lista)"** (filmes da Blender Foundation, CC BY, pelo Wikimedia
  Commons; créditos na tela de detalhes).
- Versão `1.1.0`, `versionCode = 1000 + run_number` (primeira: **1003**).
- Workflow `.github/workflows/sofae-loja.yml` + `conferir-loja.py`: o build
  **falha sozinho** se o pacote, a versão ou o certificado não baterem, se
  houver permissão proibida ou texto de pagamento no `libapp.so`.
- Artifacts: `Sofae-Loja-AAB` (Play) e `Sofae-Loja-APK-Amazon`.
- Assinatura: mesma chave de envio do painel, pelos secrets
  `KEYSTORE_BASE64` / `KEYSTORE_PASSWORD` / `KEY_ALIAS` (valores no GitHub).

## Versão Windows (`sofae-windows`)

- Workflow `.github/workflows/sofae-windows.yml` (só push na branch,
  `windows-latest`, sem secrets). Marca aplicada por `sed` só no CI.
- Gera `Sofae-Windows.zip` (≈33 MB, com DLLs do VC++) e `Sofae-APK-Teste`
  (`com.sofae.app.teste`, assinatura de debug).
- Player: media_kit/libmpv — toca HLS e `.ts` ao vivo no Windows.
- Testado: canais, filmes e séries tocam direto do PC (como o Zuxo).
- Versão visível no app: "Sofae v1.0.0+N".
- Aviso de nova versão lê `https://app.sofae.com.br/windows-version.json`.
- **Instalador público (desde 19/11):** cada push na `sofae-windows` gera `Sofae-Setup.exe`
  (Inno Setup, por usuário, sem admin) e republica a release fixa `sofae-windows`
  (`--latest=false`). Link que não muda:
  `https://github.com/Jacao010706/simanplay-iptv-app/releases/download/sofae-windows/Sofae-Setup.exe`
- Sem assinatura digital: Edge/SmartScreen avisa ("normalmente não é baixado"). Cliente usa
  a setinha ao lado de "Excluir" → **Manter mesmo assim**; depois "Mais informações" →
  **Executar assim mesmo**. Some com Microsoft Store ou certificado de código.

### Melhorias feitas na `sofae-windows` (valem para todas as plataformas)

1. User-Agent `VLC/3.0.20 LibVLC/3.0.20` no player e na API.
2. Uma chamada `get_live_streams` por tipo (antes: 1 por categoria, ~51 seguidas).
3. Conta recusada (`auth 0`) vira mensagem clara; **erro nunca mostra URL/usuário/senha**.
4. Uma tentativa por fonte, 3 s entre fontes (contas de 1 conexão).
5. Ao Vivo só com canais: filtro por `stream_type` + categorias da API.
   M3U com credenciais usa a API Xtream; M3U sem credenciais descarta
   `/movie/`, `/series/` e arquivos de vídeo. Ver [[armadilhas/m3u-mistura-vod]].
6. Aba Jogos com **plano B**: monta os jogos a partir da lista do cliente
   (eventos com data + grade `xmltv.php`), escudos via TheSportsDB, sem placar.
   Ver [[decisoes/2026-11-15-jogos-plano-b]].

> As melhorias **não** estão na `main`. Levar para as outras marcas só
> depois de testar marca por marca.

## Web (`app.sofae.com.br`)

- HTML/JS/CSS puro em `/root/sofae-webapp` (no VPS), deploy com `vercel --prod`
  de dentro da pasta. Projeto Vercel `sofae-web` (conta `akitemtech-3632`).
- Service worker: subir a versão (`sofae-vN`) a cada deploy de JS. Ver
  [[armadilhas/service-worker-cache]]. Em 14/11: `sofae-v8`.
- Filmes e séries tocam. **Canais ao vivo** do provedor de teste nunca vão
  tocar no navegador: ver [[armadilhas/iptv-bloqueia-datacenter]].
  Depois de 20 s ou de falhar, mostra mensagem + botão "Baixar o app Sofae"
  (`APP_DOWNLOAD_URL` em `js/app.js`, hoje aponta para `sofae.com.br`).
- Logs do player só com `localStorage.sofaeDebug = '1'`.

## Lojas

Ver [[sistemas/lojas-de-apps]].

## Pendências

- [ ] Resultado da revisão: Google Play (enviado 18/11) e Amazon (enviado 17/11)
- [ ] Depois de aprovado: trocar `APP_DOWNLOAD_URL` da web pelos links das lojas
- [x] Página de download do Sofae (19/11): `simanplay-iptv-admin-panel.vercel.app/baixar.html?brand=Sofae&cor=ff8a1a`
  → Android/Fire TV = APK white-label (`/api/dl/8794079`), Windows = `Sofae-Setup.exe`.
  Tabela `MARCAS` no `public/baixar.html` (painel, merge `049e820` autorizado). Outras marcas: links de sempre.
- [ ] Microsoft Store (MSIX assinado) para a versão Windows
- [ ] Declarar status de comerciante no Play Console (prazo: fev/2027)
- [ ] Separar o `applicationId` do APK direto (hoje igual ao da loja) — ver [[decisoes/2026-11-16-sofae-lojas-gratuito]]
- [ ] Repositório público `Jacao010706/sofae-tmp` (criado no dia 14 para passar arquivo) — apagar
- [ ] Mesclar as melhorias da `sofae-windows` na `main` (com teste por marca)
- [ ] Aba Jogos com placar depende da API-Football voltar — ver [[sistemas/apifootball-relay]]
