# Ao Vivo cheio de pastas de filmes ("FILMES: GUERRA" etc.)

## Sintoma

Na aba Ao Vivo aparecem pastas como "FILMES: TERROR" com pôsteres de
filmes, junto dos canais.

## Causa

A lista entra no app como **link M3U** (`get.php?type=m3u_plus`). No
provedor de teste o M3U traz tudo junto: ~2,4 mil canais, ~22 mil filmes e
~277 mil episódios. O app jogava tudo no Ao Vivo. O filtro por
`stream_type` da API não pegava porque a lista não passava pela API.

## Solução (build 4 da `sofae-windows`)

- M3U **com** credenciais (`username`/`password` no link): Ao Vivo usa a API
  Xtream; se a API falhar, cai no M3U filtrado sem mostrar erro.
- M3U **sem** credenciais: descartar `/movie/`, `/series/` e arquivos de
  vídeo (`.mp4 .mkv .avi ...`).
- Canais "24 horas" (`FILMES 24 HORAS`) **ficam** — são `/live/`.
- Não usar a regra "mesmo nome em `get_vod_categories` sai do Ao Vivo":
  apagaria pastas legítimas (UHD 4K, DOCUMENTARIOS, LEGENDADOS, RELIGIOSOS).
- Parse fora da interface (~1 s para 300 mil linhas).

Efeito colateral: favoritos do Ao Vivo salvos antes nessas listas somem
(o id do canal mudou), mas os canais ganham EPG.
