# Battery Status – Mi Band 4

Characteristic UUID: 00000006-0000-3512-2118-0009af100700  
Service UUID: 0000fee0-0000-1000-8000-00805f9b34fb  

## Payload observado (baseline)

Fonte: `logs/2026-01-31_baseline.log`


0f5100b207010100000000ea07011f0b292fec63


Tamanho: 19 bytes

---

## Estrutura inicial (v0.1 – anotações)

| Offset | HEX | Dec | Estado | Observação |
|------|----|----|------|-----------|
| 0 | 0f | 15 | CONFIRMADO | Bateria (%) |
| 1 | 51 | 81 | HIPÓTESE | Estado de carga |
| 2 | 00 | 0 | CONFIRMADO | Reservado |
| 3 | b2 | 178 | HIPÓTESE | Tensão / ciclos |
| 4–9 | — | — | HIPÓTESE | Desconhecido |
| 10–16 | ea07011f0b292f | — | INFERIDO | Timestamp |
| 17–18 | ec63 | — | HIPÓTESE | Flags / CRC |

---

## Payload observado (carregando)

Fonte: `logs/2026-02-01_battery_charging.log`


---

## Diferenças observadas (baseline × carregando)

| Offset | Baseline | Carregando | Estado |
|--------|----------|------------|--------|
| 1 | 0x51 (81) | 0x63 (99) | INFERIDO – Charge state |
| 2 | 0x00 | 0x01 | INFERIDO – Charging flag |

---

## Observações livres

- Byte 0 confere com o app Mi Fit
- Timestamp parece bater com horário do log
- Bytes 1 e 2 mudam exclusivamente ao conectar carregador
- Byte 2 aparenta ser flag binária de carregamento
