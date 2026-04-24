# Design & Decision Record (DDR)
**GreenField Technologies | IoT Systems Design**

**Team Members:**
1. Sebastian Tovar Jimenez
2. María José Cuadros

---

## 1. System Overview

*   **System Type:** [X] Component (Lab 1-2) | [ ] System (Lab 3-6) | [ ] Environment (Lab 7-8)
*   **Description:***   **System Type:** [x] Component (Lab 1-2)
*   **Description:**
Sistema basado en nodos ESP32-C6 utilizando comunicación IEEE 802.15.4 para redes IoT en agricultura (SoilSense). 
El objetivo es validar el desempeño del radio en términos de alcance, interferencia y confiabilidad en condiciones reales.

---

## 2. Lab Log & Stakeholder Summaries

### Lab 1: RF Characterization
*   **To Samuel (Architect):** Se realizó la     caracterización del radio 802.15.4 del ESP32-C6 midiendo RSSI y PER a diferentes distancias.

    El canal seleccionado fue el 15 con un noise floor de -106 dBm, siendo el más limpio del espectro.

    Se observó que el RSSI disminuye con la distancia, alcanzando valores de -91 dBm a 30 m (A→B), donde el PER superó el 1%.

    Se determinó que el umbral de confiabilidad está alrededor de -70 dBm, por lo que se recomienda un rango máximo confiable de 20 m con margen de seguridad.
*   **To Edwin (Ops):** Para despliegue en campo:

    - Usar canal 15 para evitar interferencias
    - Mantener nodos a máximo 20 m
    - Verificar RSSI (> -70 dBm)
    - Evitar obstáculos como paredes, vidrio y personas

    Si hay pérdida de paquetes:
    1. Revisar canal
    2. Medir RSSI
    3. Reducir distancia entre nodos

### Lab 2: 6LoWPAN
*   **To Samuel:**

### Lab 3: Thread & CoAP
*   **To Daniela (Customer):**

### Lab 4: Sensors & Control
*   **To Edwin:**

### Lab 5: Border Router
*   **To Daniela:**

### Lab 6: Security
*   **To Edward (Security):**

### Lab 7: Dashboard
*   **To Gustavo (Product):**

### Lab 8: Final Integration
*   **To All:**

---

## 3. Architecture Decision Records (ADRs)

**ADR-001: Selección de canal 802.15.4**
*   **Context:** Se requiere seleccionar el canal con menor interferencia en la banda de 2.4 GHz para garantizar comunicación confiable.

*   **Decision:** Se selecciona el canal 15.
*   **Rationale:** El canal 15 presentó el menor nivel de ruido (-106 dBm), lo que indica menor interferencia comparado con otros canales como 26, 18, 12, 11 y 13.
Esto mejora la relación señal/ruido (SNR) y reduce la pérdida de paquetes.

*   **Status:** [ ] Proposed | [ X ] Accepted | [ ] Deprecated

---

## 4. ISO/IEC 30141 Mapping

### Domain Mapping

| Component           | ISO Domain | Justification |
|--------------------|------------|--------------|
| ESP32-C6           | SCD        | Dispositivo que procesa y comunica datos |
| Radio 802.15.4     | SCD        | Permite la comunicación entre nodos |
| Antena             | SCD        | Interfaz física de comunicación |
| Aire (RF)          | PED        | Medio físico donde viaja la señal |
| Interferencia WiFi | PED        | Fenómeno físico |
|                     |                             |

### Component Capabilities

| Capability Category | Subcategory | Component/Feature        | Active/Latent | Lab Introduced |
|---------------------|-------------|--------------------------|---------------|----------------|
| Data                | Processing  | Lectura de RSSI          | Active        | Lab 1          |
| Data                | Transferring| Radio 802.15.4           | Active        | Lab 1          |
| Interface           | Network     | Comunicación inalámbrica | Active        | Lab 1          |
| Interface           | Human UI    | Monitor serial           | Active        | Lab 1          |
| Supporting          | Security    | Hardware crypto          | Latent        | Lab 1          |
| Latent              | —           | WiFi/BLE                 | Latent        | Lab 1          |
| Transducer          | Actuating   | LED                    | Active        | Lab 1   |

---

## 5. First Principles Reflections

**Lab 1:**

1. La señal se debilita con la distancia porque las ondas se dispersan en el espacio. 
A mayor distancia, la energía se reparte en un área más grande, por lo que llega menos potencia al receptor.

2. Aunque el receptor detecta hasta -100 dBm, no es suficiente porque hay ruido, interferencia y obstáculos. 
Se necesita un margen de seguridad (fade margin) para evitar pérdida de paquetes.

3. El radio usa técnicas como DSSS que distribuyen la señal en varias frecuencias, lo que ayuda a reducir el efecto de interferencia.

**Lab 2:**
1.

...

---

## 6. Performance Baselines

| Metric | Target | Measured | Status |
|--------|--------|----------|--------|
| Lab 1: Max Range | > 20m | 30 m | [ X ] Pass |
| Lab 2: Healing Time | < 120s | ___ s | [ ] Pass |
| Lab 3: CoAP Latency | < 200ms| ___ ms | [ ] Pass |
| Lab 4: Poll Latency | < 5s | ___ s | [ ] Pass |
| Lab 6: DTLS Time | < 3s | ___ s | [ ] Pass |

---

## 7. Ethics & Sustainability Checklist

*   [ X ] **Lab 1:** Verified interference doesn't disrupt neighbors.


| Distance | RSSI A→B | RSSI B→A |
|----------|----------|----------|
| 1 m      | -43 dBm  | -42 dBm  |
| 5 m      | -44 dBm  | -40 dBm  |
| 10 m     | -69 dBm  | -60 dBm  |
| 20 m     | -76 dBm  | -66 dBm  |
| 30 m     | -91 dBm  | -86 dBm  |
|          |          |          |
Conclusión clave:

PER > 1% a 30 m (A→B)
Rango confiable: 20 m

*   [ ] **Lab 4:** Data collection minimized (Privacy).
*   [ ] **Lab 5:** System works locally without cloud (Sustainability).
*   [ ] **Lab 6:** Encryption enabled (Privacy).
*   [ ] **Lab 8:** End-of-Life plan considered.

---

## 8. Viewpoint Analysis

| Viewpoint | Labs Addressed | Key Concerns Documented |
|-----------|----------------|-------------------------|
| Foundational |            |                         |
| Business |               |                         |
| Usage |                  |                         |
| Functional |             |                         |
| Trustworthiness |        |                         |
| Construction |           |                         |

---

## 9. Trustworthiness Audit (Lab 6+)

| Characteristic | Addressed? | How | Gaps |
|----------------|------------|-----|------|
| Availability |            |     |      |
| Confidentiality |         |     |      |
| Integrity |               |     |      |
| Reliability |             |     |      |
| Resilience |              |     |      |
| Safety |                  |     |      |
| Compliance |              |     |      |

---

## 10. Construction Viewpoint - IoT System Pattern (Lab 8)

| Pattern Element | Category | Your System |
|-----------------|----------|-------------|
| IoT System |            |             |
| IoT Components |         |             |
| Digital Network |        |             |
| IoT Devices |            |             |
| Primary Capability (observation) | |   |
| Primary Capability (control) | |       |
| Secondary Capability (processing) | |  |
| Secondary Capability (transferring) | | |
| Secondary Capability (storage) | |     |
| Interface (network) |    |             |
| Interface (human UI) |   |             |
| Interface (application) | |            |
| Supplemental (security) | |            |
| Supplemental (orchestration) | |       |
| Supplemental (management) | |          |