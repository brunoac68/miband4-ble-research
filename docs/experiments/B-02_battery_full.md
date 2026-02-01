# Experimento B-02 — Bateria cheia (Mi Band 4)

## Objetivo
Identificar e confirmar a estrutura do payload de bateria
em estado de carga completa (100%), comparando estados
plugado e desplugado.

---

## Ambiente
- Dispositivo: Mi Band 4
- Conexão: BLE (BlueZ + bleak)
- Data: 2026-02-01
- Script: tools/collectors/miband4_test_suite.py

---

## Logs utilizados
- logs/2026-01-31_baseline.log
- logs/2026-02-01_battery_charging.log
- logs/2026-02-01_battery_full_plugged.log
- logs/2026-02-01_battery_full_unplugged.log

---

## Payloads observados

### FULL + Plugged

0f6301ea070201011a3becea070201012e02ec64


### FULL + Unplugged


0f6300ea070201011a3becea070201013413ec63


---

## Análise byte a byte

| Offset | Plugged | Unplugged | Interpretação | Status |
|------|---------|-----------|--------------|--------|
| 0 | 0f | 0f | Tipo de frame | HIPÓTESE |
| 1 | 63 | 63 | Estado energético | CONFIRMADO |
| 2 | 01 | 00 | Flag de carregamento | CONFIRMADO |
| 3–16 | — | — | Timestamp / estado interno | INFERIDO |
| 17–18 | ec64 / ec63 | CRC / checksum | HIPÓTESE |

---

## Conclusões

- Byte 2 é uma flag binária de carregamento
- Byte 1 representa um estado energético codificado
- Byte 0 **não** representa percentual de bateria
- Percentual exibido no app é derivado internamente

---

## Estado do experimento
🟢 **FECHADO**

