# Explotación de vulnerabilidad

## Objetivo

Investigar un intento o explotación exitosa de una vulnerabilidad en un servicio, aplicación o sistema, y determinar si hubo compromiso posterior.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0001 Initial Access | T1190 Exploit Public-Facing Application |
| TA0002 Execution | T1203 Exploitation for Client Execution |
| TA0003 Persistence | T1505.003 Web Shell |
| TA0004 Privilege Escalation | T1068 Exploitation for Privilege Escalation |

## Severidad orientativa

- **Low/Medium**: intento bloqueado (WAF/IPS) contra activo no vulnerable.
- **High**: intento contra activo vulnerable sin confirmación de éxito, o explotación con impacto limitado.
- **Critical**: explotación exitosa con ejecución de código, webshell o acceso, especialmente en activo expuesto o crítico.

## Fuentes de datos

- IDS/IPS/WAF: firma, payload, veredicto (bloqueado/permitido).
- Logs del servicio (web access/error logs, aplicación): respuesta al intento (códigos 200 vs 4xx/5xx, tamaño de respuesta).
- EDR del activo: procesos hijos del servicio (un servidor web lanzando cmd/bash/powershell = explotación casi segura).
- Gestión de vulnerabilidades: ¿el activo es vulnerable al CVE? ¿parche aplicado y cuándo?
- Threat intel: ¿CVE con explotación activa conocida (KEV)?

---

## Datos

| Campo | Valor |
|---|---|
| Activo afectado (¿expuesto a Internet?) | |
| Servicio y versión | |
| CVE / vulnerabilidad | |
| ¿Activo vulnerable? (versión/parche verificado) | |
| IP(s) origen | |
| Payload observado | |
| Resultado (bloqueado / permitido / desconocido) | |
| Timestamp (UTC) | |

---

## Pasos de investigación

1. Verificar aplicabilidad: versión del servicio vs versiones vulnerables del CVE. Si no es vulnerable y fue bloqueado → documentar y cerrar rápido.
2. Analizar el payload y la respuesta del servidor: ¿el intento obtuvo respuesta de éxito (200/estructura esperada por el exploit)?
3. Buscar **evidencia de post-explotación en el activo** (lo decisivo):
   - Procesos hijos anómalos del servicio (webserver → shell).
   - Ficheros nuevos en rutas web (webshells: .jsp/.aspx/.php recientes).
   - Cuentas creadas, tareas/cron nuevos, conexiones salientes del servidor.
4. Reconstruir toda la actividad de la IP atacante contra el activo (antes: reconocimiento; después: uso del acceso) y contra el resto del parque.
5. Comprobar si el ataque es masivo/oportunista (escaneo de Internet del CVE de moda) o dirigido.
6. Verificar exposición y parcheo del resto de activos con el mismo servicio.

---

## Evidencias

| Timestamp (UTC) | Origen | Destino | Servicio | Payload/Detección | Respuesta del servidor | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿La vulnerabilidad aplica realmente al activo (versión, configuración)?
- ¿El intento fue bloqueado o llegó a la aplicación?
- ¿Hay evidencia de ejecución posterior (procesos, webshell, cuentas, conexiones salientes)?
- ¿El activo está parcheado? ¿Desde cuándo era vulnerable estando expuesto?
- ¿Hay más activos con el mismo servicio vulnerable?
- ¿La IP atacante ha tocado otros activos?
- ¿Debe aislarse o parchearse urgentemente?

## Falsos positivos habituales

- Escáneres de vulnerabilidades (propios o de terceros contratados) y pentest autorizado.
- Escaneo masivo de Internet sin éxito contra activos no vulnerables (documentar, no escalar).
- Firmas IDS genéricas disparando sobre tráfico legítimo (payloads en parámetros normales).

---

## Contención recomendada (si se confirma explotación)

- [ ] Aislar el activo (o restringir a lo imprescindible si es servicio crítico)
- [ ] Eliminar webshell/persistencia tras preservar evidencia
- [ ] Bloquear IP(s) atacante(s)
- [ ] Parchear o mitigar (WAF virtual patching) antes de reexponer
- [ ] Rotar credenciales y secretos del servicio y del host
- [ ] Revisar y parchear el resto de activos con el mismo servicio

## Observables a extraer (TheHive)

ip (atacante), url (payload/exploit), hash y filename (webshell/payload), hostname, other (CVE).

---

## Veredicto

- [ ] Intento bloqueado / activo no vulnerable
- [ ] Intento contra activo vulnerable sin éxito confirmado (vigilancia + parcheo urgente)
- [ ] Explotación exitosa (→ incidente)
- [ ] Escáner/pentest autorizado
- [ ] Falso positivo
