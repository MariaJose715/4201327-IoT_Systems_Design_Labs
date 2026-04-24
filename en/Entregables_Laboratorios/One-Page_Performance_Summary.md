### 2. One-Page Performance Summary


**GreenField SoilSense - Lab 1 Performance Report**

**Objective**: Test if ESP32-C6 radio works for farm sensor networks

**Key Findings**:
- ✅ Maximum reliable range: **20m** (packet loss < 1% when RSSI > **-70 dBm**)
- ✅ Recommended sensor spacing: **-70m** (includes safety margin for vegetation/obstacles)
- ✅ Best radio channel: **802.15.4 Channel 15** (least interference: -106 dBm noise floor)
- ⚠️ Risk: WiFi interference detected on channels 26, 18, 12, 11, 13 (avoid deploying sensors near these)

**Impact on Product**:
- For a 10-hectare farm field: approximately **25 sensor nodes** required
- Estimated hardware cost: 25 nodes × $40/node = **$1000 USD**

**Recommendation**: [Choose one]
- ✅ **Proceed** - ESP32-C6 meets requirements
- ⚠️ **Need more testing** - Explain what concerns remain
- ❌ **Switch platforms** - Explain why ESP32-C6 isn't suitable

---

**Keep it simple!** Use bullet points, not paragraphs. Gustavo wants numbers and clear recommendations.

---

