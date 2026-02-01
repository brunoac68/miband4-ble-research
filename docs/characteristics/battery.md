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

---

## Estado atual da engenharia reversa

### Confirmado
- Byte 2: flag de carregamento (01/00)
- Byte 1: estado energético codificado

### Refutado
- Byte 0 como percentual de bateria

### Experimentos relacionados
- B-01 (charging)
- B-02 (full)

---

# Battery Characteristic — Mi Band 4

UUID: 00000006-0000-3512-2118-0009af100700  
Service: 0000fee0-0000-1000-8000-00805f9b34fb  

---

## Estados analisados

| Sigla | Estado físico |
|-----|--------------|
| BL | Baseline (descarregando) |
| CH | Carregando (<100%) |
| FP | Full Plugged (100%, carregador conectado) |
| FU | Full Unplugged (100%, carregador removido) |

---

## Comparativo byte a byte (estado × payload)

| Offset | BL | CH | FP | FU | Interpretação | Status |
|------|----|----|----|----|--------------|--------|
| 0 | 0f | 0f | 0f | 0f | Identificador / tipo de frame | HIPÓTESE |
| 1 | 51 | 63 | 63 | 63 | Estado energético codificado | CONFIRMADO |
| 2 | 00 | 01 | 01 | 00 | Flag de carregamento | CONFIRMADO |
| 3–9 | — | — | — | — | Dados internos | DESCONHECIDO |
| 10–16 | ✔ | ✔ | ✔ | ✔ | Timestamp interno | INFERIDO |
| 17–18 | ec63 | ec63 | ec64 | ec63 | CRC / assinatura | HIPÓTESE |

---

## Conclusões consolidadas

- Byte 2 representa inequivocamente o estado de carregamento
- Byte 1 representa um estado energético interno
- Byte 0 **não** representa percentual de bateria
- Percentual exibido no app é derivado internamente

---

## Evidências experimentais

- B-01 — bateria em carga
- B-02 — bateria cheia (plugado × desplugado)

Ver detalhes em:
- `docs/experiments/B-02_battery_full.md`
