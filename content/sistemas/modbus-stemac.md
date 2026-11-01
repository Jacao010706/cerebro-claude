# Modbus — STEMAC ST2160

Decodificado a partir do manual `MAN_670.060.0140_V100R03`.
Validado ao vivo no GMG-ANCHIETA (10.80.0.6). Login confirmado nas
10 unidades ST2160.

## Registradores

| Endereço | Função |
|---|---|
| `4x0001` bit 2 | Start / Stop |
| `4x0001` bit 3 | Reconhece alarmes |
| `4x0001` bit 4 | Modo remoto |
| `4x0001` bit 12 | Parada remota |
| `4x0003` / `4x0004` / `4x0005` | Login nível 5: escrever `0`, `0`, `4567` |
| `FC04 3x1000` (end. 999) | Verifica login — bits 0 e 1 devem estar zerados |
| `IR[62]` | `is_running` se maior que zero |

## Sequências

```
PARTIDA   login → pulso bit 4 → aguarda 1 s → pulso bit 2
PARADA    login → pulso bit 12
```

## Pegadinha confirmada

O registrador **56 não é** o indicador de funcionamento — é o horímetro.
Foi candidato errado durante a decodificação. Use `IR[62]`.

## Onde está o código

`modbus_command.py`, commit `aac0e77`. Contém os drivers DSE e STEMAC.

## Status

O comando remoto STEMAC está **totalmente resolvido**. Ao retomar
trabalho nessa área, assuma que funciona.
