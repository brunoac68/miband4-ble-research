# B-03 — Battery Discharge Curve (Mi Band 4)

## Descrição
Experimento para mapear a descarga da bateria da Mi Band 4,
correlacionando percentual exibido com payload BLE da characteristic proprietária.

---

## Estado registrado: D95 (95%)

### Identificação
- **Código:** B-03_D95
- **Data:** 2026-02-01
- **Hora aproximada:** 10:38
- **Percentual exibido no dispositivo:** 95%
- **Carregador:** NÃO conectado

---

### Contexto físico (estado real)
- Dispositivo em uso normal
- Atividade recente: limpeza de piscina
- Movimento moderado a intenso
- Nenhum reset ou reconexão forçada
- Continuidade direta após estado FULL (100%)

---

## Característica analisada

- **Service UUID:** `0000fee0-0000-1000-8000-00805f9b34fb`
- **Characteristic UUID:** `00000006-0000-3512-2118-0009af100700`
- **Acesso:** read, notify

---

## Payload observado

Fonte:

logs/2026-02-01_B-03_D95_95pct.log


Payload principal:

0f5f00ea070201011a3becea070201013413ec63


Tamanho: 19 bytes

---

## Decodificação (estado atual)

| Offset | HEX | Dec | Estado | Interpretação |
|------|----|----|------|----------------|
| 0 | 0f | 15 | CONFIRMADO | Percentual da bateria (95%) |
| 1 | 5f | 95 | CONFIRMADO | Valor correlacionado ao percentual |
| 2 | 00 | 0 | CONFIRMADO | Flag de carregamento (0 = descarregando) |
| 3 | ea | — | HIPÓTESE | Bloco de controle / status interno |
| 4–9 | 070201011a3b | — | INFERIDO | Timestamp / contador |
| 10–16 | ecea0702010134 | — | INFERIDO | Segundo timestamp / janela |
| 17–18 | 13ec | — | HIPÓTESE | Flags finais / CRC |

---

## Comparação com estados anteriores

| Estado | Byte 0 | Byte 1 | Byte 2 |
|------|------|------|------|
| B-02_FULL_PLUGGED | 0f | 63 | 01 |
| B-02_FULL_UNPLUGGED | 0f | 63 | 00 |
| **B-03_D95** | **0f** | **5f** | **00** |

---

## Conclusões parciais

- Byte 0 representa o percentual exibido no dispositivo
- Byte 1 acompanha linearmente o percentual
- Byte 2 atua como flag binária de carregamento
- Estrutura do payload permanece estável após uso real
- Não há ruído estrutural causado por atividade física

---

## Status do experimento
- [x] D100 (FULL)
- [x] D95
- [ ] D90
- [ ] D80
- [ ] D70
- [ ] D50
- [ ] D30
- [ ] D10

