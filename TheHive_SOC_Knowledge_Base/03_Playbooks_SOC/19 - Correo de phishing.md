# Correo de phishing

## Objetivo

Investigar correo sospechoso (credenciales, adjuntos maliciosos, URLs fraudulentas, fraude BEC), determinar quién lo recibió, quién interactuó y contener la campaña.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0001 Initial Access | T1566.001 Spearphishing Attachment|
||T1566.002 Spearphishing Link |
| TA0006 Credential Access | T1598 Phishing for Information |
| TA0002 Execution | T1204 User Execution |

## Severidad orientativa

- **Low/Medium**: correo reportado, sin clics ni entrega masiva.
- **High**: hubo clic + introducción de credenciales, o adjunto ejecutado, o campaña a muchos buzones.
- **Critical**: credenciales de cuenta privilegiada comprometidas, o BEC con fraude económico en curso.

## Fuentes de datos

- Gateway de correo: trazas de entrega (destinatarios totales de la campaña), veredictos, cabeceras.
- Cabeceras del correo original (pedir el .eml/.msg, no el reenvío).
- Proxy/DNS/EDR: clics en la URL, descargas, ejecución del adjunto.
- Identidad: logins tras el clic (correlacionar con playbook 03).

---

## Datos

| Campo | Valor |
|---|---|
| Remitente (From visible) | |
| Remitente real (Return-Path / envelope) | |
| Reply-To (si difiere: señal de fraude) | |
| IP de envío y resultado SPF/DKIM/DMARC | |
| Destinatario(s) inicial(es) | |
| Asunto | |
| URL(s) (y destino final tras redirecciones) | |
| Adjunto (nombre, tipo, hash) | |
| Timestamp de entrega (UTC) | |

---

## Pasos de investigación

1. Obtener el correo original (.eml) y analizar cabeceras: SPF/DKIM/DMARC, IP origen, dominio remitente (¿typosquatting? ¿dominio legítimo comprometido? ¿servicio de mailing?).
2. Analizar URL en entorno seguro (sandbox/analyzer, nunca en el equipo del analista; respetar PAP): destino final, ¿página de robo de credenciales imitando la corporativa?
3. Analizar adjunto: tipo real, hash, sandbox/detonación.
4. **Dimensionar la campaña**: buscar en el gateway el mismo remitente/asunto/URL/hash → lista completa de destinatarios.
5. **Identificar interacción**: quién hizo clic (proxy/DNS), quién introdujo credenciales (POST a la página, logins sospechosos posteriores), quién ejecutó el adjunto (EDR).
6. Para cada usuario que introdujo credenciales: aplicar playbook `03 - Sospecha de toma de cuenta.md`.
7. Para cada ejecución de adjunto: aplicar playbook `11 - Malware detectado.md`.
8. Si es BEC (fraude sin malware): revisar hilo completo, cuentas bancarias solicitadas, y si hubo pago → escalar a dirección/legal/banco de inmediato.

---

## Evidencias

| Timestamp (UTC) | Remitente | Destinatario | Asunto | IOC (URL/hash) | Interacción (clic/credenciales/ejecución) | Acción |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿El remitente es suplantado (spoofing/typosquatting) o una cuenta legítima comprometida?
- ¿SPF/DKIM/DMARC pasan? (que pasen no garantiza legitimidad si el dominio es del atacante)
- ¿Cuántos buzones recibieron la campaña?
- ¿Quién hizo clic, introdujo credenciales o ejecutó el adjunto?
- ¿Hay logins sospechosos posteriores de los afectados?
- ¿Hay reglas de buzón o reenvíos creados después?
- ¿Es parte de una campaña conocida (threat intel)?

## Falsos positivos habituales

- Marketing legítimo agresivo o mal configurado (SPF/DKIM fallando en remitente real).
- Simulacros de phishing internos (verificar con el equipo de concienciación antes de contener).
- Correos legítimos con acortadores o dominios de terceros (docusign, mailchimp).

---

## Contención recomendada (si se confirma)

- [ ] Purgar el correo de **todos** los buzones receptores (no solo del que reportó)
- [ ] Bloquear remitente/IP en el gateway y URL/dominio en proxy/DNS
- [ ] Bloquear hash del adjunto en EDR
- [ ] Resetear credenciales + revocar sesiones de quienes las introdujeron (→ playbook 03)
- [ ] Notificar a los destinatarios con indicaciones claras
- [ ] Reportar el sitio de phishing para takedown si procede

## Observables a extraer (TheHive)

mail (remitente), mail-subject, url, domain, ip (envío), hash y filename (adjunto), user-agent.

---

## Veredicto

- [ ] Phishing confirmado sin interacción
- [ ] Phishing con credenciales comprometidas (→ playbook 03)
- [ ] Phishing con malware ejecutado (→ playbook 11)
- [ ] BEC / fraude (→ escalado dirección/legal)
- [ ] Simulacro interno
- [ ] Correo legítimo / falso positivo
