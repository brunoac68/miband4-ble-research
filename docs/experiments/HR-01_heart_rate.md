# HR-01 — Heart Rate Reverse Engineering (Mi Band 4)

Este experimento documenta a coleta, análise e engenharia reversa
dos dados de **frequência cardíaca (Heart Rate)** transmitidos pela Mi Band 4 via BLE.

---

## 📌 Identificação do Experimento

- **ID:** HR-01  
- **Subteste:** HR-01a  
- **Data:** 2026-02-01  
- **Dispositivo:** Mi Band 4  
- **Interface:** Bluetooth Low Energy (BLE)

---

## 🎯 Objetivo

- Identificar quais **characteristics BLE** transmitem dados de batimento cardíaco
- Documentar o **payload em HEX**
- Correlacionar valores com **BPM real**
- Verificar comportamento de **notify vs read**
- Analisar impacto de estado físico (repouso, movimento, esforço)

---

## 🧪 Condições do Teste (HR-01a)

| Parâmetro | Valor |
|---------|------|
| Postura | Sentado |
| Movimento | Nenhum |
| Estado físico | Repouso |
| Atividade anterior | Nenhuma |
| Duração | ~2 minutos |
| Ambiente | Residencial |
| Bateria | ~95% |

---

## 🗂 Log Utilizado

logs/2026-02-01_HR-01_rest.log


---

## 🔍 Services & Characteristics Relevantes

### Heart Rate Service (GATT Standard)

- **Service UUID:** `0000180d-0000-1000-8000-00805f9b34fb`

| Characteristic | UUID | Propriedades |
|---------------|------|--------------|
| Heart Rate Measurement | `00002a37-0000-1000-8000-00805f9b34fb` | notify |
| Heart Rate Control Point | `00002a39-0000-1000-8000-00805f9b34fb` | read, write |

---

## 📦 Payload Observado (Notify)

Exemplo de notificações capturadas:


00002a37 → 0044
00002a37 → 0044
00002a37 → 004c
00002a37 → 004b


---

## 🧠 Decodificação Inicial (v0.1)

| Byte(s) | HEX | Decimal | Interpretação | Estado |
|-------|-----|--------|--------------|--------|
| 0–1 | 00 44 | 68 | Heart Rate (BPM) | CONFIRMADO |
| 0–1 | 00 4C | 76 | Heart Rate (BPM) | CONFIRMADO |
| 0–1 | 00 4B | 75 | Heart Rate (BPM) | CONFIRMADO |

> Interpretação em **big-endian**, compatível com GATT Heart Rate Profile.

---

## ⚠️ Comportamento Observado

- Notify em `00002a37` ocorre **apenas quando sensor está ativo**
- Leitura direta (`read`) **não é permitida**
- Notificações podem falhar se já estiverem adquiridas por outro processo
- HR não inicia automaticamente apenas com subscribe

---

## 🧩 Limitações Identificadas

- Falha frequente:

[org.bluez.Error.NotPermitted] Notify acquired

- Indica que a Mi Band:
- exige comando prévio
- ou bloqueia múltiplos subscribers

---

## 📌 Hipóteses Atuais

| ID | Hipótese | Estado |
|----|---------|--------|
| H-01 | Payload contém apenas BPM (uint16) | CONFIRMADA |
| H-02 | Endianness é big-endian | CONFIRMADA |
| H-03 | Start HR exige comando proprietário | EM INVESTIGAÇÃO |
| H-04 | Sensor HR é mutuamente exclusivo | EM INVESTIGAÇÃO |

---

## 🔜 Próximos Subtestes Planejados

- **HR-01b:** Caminhada leve (movimento contínuo)
- **HR-01c:** Pós esforço físico
- **HR-02:** Streaming contínuo de HR + timestamps

---

## 📚 Referências

- Bluetooth SIG — Heart Rate Profile
- Logs do experimento HR-01a
- TEST_MATRIX.md

