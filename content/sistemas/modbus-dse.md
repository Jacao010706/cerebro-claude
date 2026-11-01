# Modbus — DSE (protocolo Gencomm)

## Registradores

| Registrador | Leitura |
|---|---|
| `1030` | RPM — `is_running` se maior que zero |
| `1065` | Tensão L1 |
| `FC16 4104 / 4105` | Escrita de comando |

## Onde está o código

`modbus_command.py`, commit `aac0e77`.
