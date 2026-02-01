## Teste B-01 – Bateria em carregamento

Log: logs/2026-02-01_battery_charging.log

### Hipótese
Byte 1 e/ou 2 indicam estado de carga.

### Resultado
- Byte 1: 0x51 → 0x63
- Byte 2: 0x00 → 0x01

### Conclusão
- Byte 2 é flag de carregamento
- Byte 1 é estado codificado de carga
