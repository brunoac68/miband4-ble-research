# Test Matrix — Mi Band 4 BLE Research

Este documento centraliza **todos os experimentos planejados, em execução e concluídos**
para engenharia reversa e validação das characteristics BLE da Mi Band 4.

---

## 🪫 Battery Experiments

| ID | Descrição | Condição | Status | Logs | Documento |
|----|----------|---------|--------|------|-----------|
| B-01 | Charging baseline | Bateria < 100%, carregando | ✅ Done | 2026-01-31_baseline.log | B-01_battery_charging.md |
| B-02a | Full battery (plugged) | 100%, conectado ao carregador | ✅ Done | 2026-02-01_battery_full_plugged.log | B-02_battery_full.md |
| B-02b | Full battery (unplugged) | 100%, removido do carregador | ✅ Done | 2026-02-01_battery_full_unplugged.log | B-02_battery_full.md |
| B-03_D95 | Battery discharge start | 95%, uso ativo | 🟡 Running | 2026-02-01_B-03_D95_95pct.log | B-03_battery_discharge.md |
| B-03_D90 | Battery discharge | 90%, uso normal | 🔲 Planned | — | B-03_battery_discharge.md |
| B-03_D80 | Battery discharge | 80%, uso normal | 🔲 Planned | — | B-03_battery_discharge.md |
| B-03_D50 | Battery discharge | 50%, uso normal | 🔲 Planned | — | B-03_battery_discharge.md |
| B-03_D20 | Battery discharge | 20%, uso normal | 🔲 Planned | — | B-03_battery_discharge.md |
| B-03_D05 | Battery discharge (critical) | ≤5%, uso mínimo | 🔲 Planned | — | B-03_battery_discharge.md |

---

## ❤️ Heart Rate Experiments

| ID | Descrição | Condição Física | Status | Logs | Documento |
|----|----------|----------------|--------|------|-----------|
| HR-01a | Resting heart rate | Sentado, repouso | ✅ Done | 2026-02-01_HR-01_rest.log | HR-01_heart_rate.md |
| HR-01b | Rest + movimento leve | Caminhada leve | 🔲 Planned | — | HR-01_heart_rate.md |
| HR-01c | Post-effort HR | Pós exercício | 🔲 Planned | — | HR-01_heart_rate.md |
| HR-02 | Continuous HR notify | HR ativo contínuo | 🔲 Planned | — | HR-02_continuous.md |

---

## 🔔 Notification & Streaming

| ID | Descrição | Characteristic | Status | Logs | Documento |
|----|----------|---------------|--------|------|-----------|
| N-01 | Battery notify behavior | 00000006 | 🟡 Partial | battery logs | battery.md |
| N-02 | HR notify payload | 00002a37 | 🟡 Partial | HR logs | heart_rate.md |
| N-03 | Timestamp propagation | multiple | 🔲 Planned | — | methodology.md |

---

## 🧠 Metadata & Reverse Engineering

| ID | Descrição | Fonte | Status |
|----|----------|------|--------|
| M-01 | Battery payload structure | B-01, B-02, B-03 | 🟡 Partial |
| M-02 | Charging flag validation | B-01, B-02 | ✅ Confirmed |
| M-03 | Timestamp encoding | Battery + HR | 🟡 Partial |
| M-04 | CRC / flags bytes | Battery payload | 🔲 Hypothesis |

---

## 📌 Status Legend

- ✅ **Done** — executado e documentado
- 🟡 **Running / Partial** — em andamento ou com dados parciais
- 🔲 **Planned** — planejado, ainda não executado

