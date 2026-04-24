### 3. Quick Reference for Edwin

Create a troubleshooting guide:

**SoilSense Field Deployment - RF Checklist**

**Symptom: Device won't join network**
1. Check channel matches network (use `dataset channel` command)
2. Verify antenna connected (loose connector common issue)
3. Check for metal obstructions (barns, silos block RF)

**Symptom: Intermittent packet loss**
1. Check RSSI (should be > -70 dBm for reliability)
2. Scan for WiFi interference (`scan energy 500 0xffff`)
3. Reduce node spacing if vegetation is dense

**Maximum Range Guidelines**:
- Line of sight: m
- Through light vegetation: ___m
- Through dense crops: ___m (reduce spacing)

**SoilSense Field Deployment - RF Checklist**

---

###  Problema: El dispositivo no se conecta

1. Verificar que ambos nodos estén en el mismo canal (usar `dataset channel`)
2. Revisar conexión de la antena
3. Evitar obstáculos metálicos o estructuras grandes

---

###  Problema: Pérdida intermitente de paquetes

1. Medir RSSI → debe ser mayor a **-70 dBm**
2. Escanear interferencia (`scan energy 500 0xffff`)
3. Cambiar a canal 15 si no está configurado
4. Reducir distancia entre nodos

---

###  Parámetros recomendados

* Canal: **15**
* RSSI mínimo: **-70 dBm**
* Distancia máxima recomendada: **20 m**

---

###  Guía de alcance

* Línea de vista: **20 m**
* Con obstáculos ligeros (personas, muebles): **15 m**
* Con obstáculos densos (paredes, vidrio): **10 m o menos**

---

###  Buenas prácticas

* Evitar ubicar nodos cerca de routers WiFi
* Mantener altura similar entre dispositivos
* Reducir interferencias del entorno
