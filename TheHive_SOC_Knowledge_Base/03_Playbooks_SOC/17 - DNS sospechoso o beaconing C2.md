# DNS sospechoso o beaconing C2

## Objetivo

Investigar consultas DNS anómalas, dominios DGA, túnel DNS o conexiones periódicas compatibles con mando y control (C2).

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0011 Command and Control | T1071.001 Web Protocols, T1071.004 DNS, T1568.002 DGA, T1572 Protocol Tunneling, T1573 Encrypted Channel |
| TA0010 Exfiltration | T1048.003 Exfiltration Over Unencrypted/Obfuscated Non-C2 Protocol (túnel DNS) |

## Severidad orientativa

- **Medium**: dominio raro sin confirmación de C2.
- **High**: beaconing con periodicidad clara o dominio con reputación maliciosa.
- **Critical**: C2 confirmado (proceso malicioso identificado, o múltiples hosts hacia la misma infraestructura).

## Fuentes de datos

- DNS resolver logs (consultas, tipos de registro, NXDOMAIN).
- Proxy / firewall / NetFlow: conexiones, periodicidad, volumen, JA3.
- EDR / Sysmon EID 3 + 22 (DNS query por proceso): **clave para atribuir la consulta a un proceso**.
- Threat intel: reputación y edad del dominio.

---

## Datos

| Campo | Valor |
|---|---|
| Host origen | |
| Usuario conectado | |
| Dominio / IP destino | |
| Edad y registrador del dominio | |
| Frecuencia / intervalo (y jitter) | |
| Proceso asociado (EDR/Sysmon 22) | |
| Tipo de registro DNS predominante (A, TXT, CNAME...) | |
| Timestamp primera/última vez visto (UTC) | |

---

## Pasos de investigación

1. **Atribuir la conexión a un proceso** (EDR / Sysmon): es lo que separa "dominio raro" de "malware confirmado".
2. Analizar el dominio: edad (recién registrado = sospechoso), registrador, hosting, reputación, ¿parecido a dominios legítimos (typosquatting)?
3. Analizar el patrón temporal: intervalo constante o con jitter regular, actividad 24x7 (una máquina encendida hablando de madrugada no es un usuario navegando), tamaño uniforme de peticiones.
4. Túnel DNS: subdominios largos/alta entropía, volumen anómalo de consultas, predominio de TXT/NULL, muchos subdominios únicos bajo el mismo dominio.
5. DGA: ráfagas de NXDOMAIN hacia dominios pseudoaleatorios antes de resolver uno.
6. Buscar más hosts consultando el mismo dominio/IP o la misma infraestructura (mismo ASN, mismos certificados).
7. Si hay proceso: pivotar a análisis de malware (hash, persistencia, origen) con el playbook 11.
8. Respetar el PAP antes de interactuar con la infraestructura (no resolver ni visitar si PAP alto).

---

## Evidencias

| Timestamp (UTC) | Host | Dominio / IP | Frecuencia | Protocolo | Proceso | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿Qué proceso origina las consultas/conexiones?
- ¿El dominio es reciente, dinámico o de mala reputación?
- ¿Hay periodicidad constante o jitter regular (beaconing)?
- ¿Hay señales de túnel DNS (entropía, TXT, volumen)?
- ¿Hay malware o persistencia asociada en el host?
- ¿Más hosts contactan la misma infraestructura?
- ¿Cuánto tiempo lleva ocurriendo (primera vez visto)?

## Falsos positivos habituales

- Telemetría legítima y actualizaciones (antivirus, navegadores, SaaS) con patrones periódicos perfectos.
- CDNs y dominios generados de servicios cloud (nombres "aleatorios" legítimos).
- Servicios de reputación/seguridad que resuelven dominios raros por diseño (sandbox, filtrado DNS).
- Adware/PUA: molesto y ruidoso, pero de menor prioridad que un C2 real.

---

## Contención recomendada (si se confirma)

- [ ] Aislar host(s)
- [ ] Bloquear dominio e IP (DNS sinkhole si está disponible: permite detectar más víctimas)
- [ ] Matar proceso, bloquear hash, eliminar persistencia
- [ ] Buscar toda la infraestructura relacionada (pasive DNS, certificados) y bloquearla
- [ ] Añadir IOCs a inteligencia y vigilar reincidencia

## Observables a extraer (TheHive)

domain, ip, url, hash (proceso), user-agent / JA3, other (patrón de beacon).

---

## Veredicto

- [ ] C2 confirmado (→ incidente)
- [ ] Beaconing sospechoso sin confirmar (vigilancia)
- [ ] Túnel DNS confirmado
- [ ] Telemetría/software legítimo
- [ ] PUA / adware
- [ ] Falso positivo
