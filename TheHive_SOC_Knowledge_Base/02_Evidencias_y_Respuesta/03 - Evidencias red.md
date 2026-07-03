# Evidencias de red

## Conexiones

| Timestamp (UTC) | IP origen | IP destino | Puerto | Protocolo | Bytes out / in | Resultado | Fuente |
|---|---|---|---|---|---|---|---|
| | | | | | | | |

---

## DNS / HTTP / TLS

| Timestamp (UTC) | Host origen | Dominio / SNI / URL | IP destino | User-Agent / JA3 | Observación |
|---|---|---|---|---|---|
| | | | | | |

> Señales de alerta: dominios recién registrados, alta entropía en subdominios (posible túnel DNS/DGA), TXT queries masivas, certificados autofirmados, User-Agents anómalos, tráfico TLS a IPs sin SNI.

---

## IDS / NDR

| Timestamp (UTC) | Firma / Detección | Severidad | Origen | Destino | Observación |
|---|---|---|---|---|---|
| | | | | | |

---

## Análisis de beaconing

- Intervalo entre conexiones (¿constante o con jitter?):
- Tamaño de paquetes (¿uniforme?):
- Horario (¿24x7 o solo horario laboral?):
- Volumen total transferido:

---

## Preguntas

- ¿Hay comunicación externa sospechosa? ¿A qué ASN / país / hosting?
- ¿Hay patrón periódico compatible con beaconing?
- ¿Hay escaneo (muchos destinos/puertos desde un origen)?
- ¿Hay explotación (firmas IDS, payloads en HTTP)?
- ¿Hay transferencia anómala de datos (volumen saliente >> entrante)?
- ¿El destino tiene mala reputación? (documentar fuente de reputación y fecha de consulta)
- ¿Qué proceso del endpoint originó la conexión? (correlacionar con EDR/Sysmon EID 3)

---

## Conclusión red

- Tráfico confirmado como malicioso:
- Tráfico descartado:
- IOC de red extraídos (pasarlos a `04 - Observables e IOCs.md`):
- Acción recomendada (bloqueo, monitorización, captura completa):
