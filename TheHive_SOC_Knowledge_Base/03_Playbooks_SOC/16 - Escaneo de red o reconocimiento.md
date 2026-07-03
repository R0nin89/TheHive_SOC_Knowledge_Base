# Escaneo de red o reconocimiento

## Objetivo

Investigar escaneo de puertos, enumeración de servicios o reconocimiento interno/externo, y valorar si es la fase previa de un ataque en curso.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0043 Reconnaissance | T1595 Active Scanning |
| TA0007 Discovery | T1046 Network Service Discovery|
||T1018 Remote System Discovery|
||T1087 Account Discovery |

## Severidad orientativa

- **Low**: escaneo externo bloqueado en perímetro (ruido de Internet).
- **Medium**: escaneo interno sin autorización aparente.
- **High**: escaneo **interno desde un host de usuario** (fuerte indicio de compromiso del origen) o escaneo seguido de intentos de explotación/login.

## Fuentes de datos

- Firewall / NetFlow: conexiones por origen (nº destinos, nº puertos, SYN sin respuesta).
- IDS/NDR: firmas de escaneo, herramientas identificadas (nmap, masscan).
- EDR del host origen (si es interno): qué proceso genera las conexiones.
- AD/LDAP: enumeración de cuentas y grupos (herramientas tipo BloodHound generan patrones LDAP característicos).

---

## Datos

| Campo | Valor |
|---|---|
| IP origen (¿host interno? ¿de usuario o servidor?) | |
| IP destino / rango | |
| Puertos (¿pocos y dirigidos o barrido completo?) | |
| Protocolo | |
| Sensor / firma | |
| Ritmo (agresivo vs low & slow) | |
| Timestamp (UTC) | |

---

## Pasos de investigación

1. Caracterizar el escaneo: horizontal (un puerto, muchos hosts: busca un servicio concreto, p. ej. 445/3389/22) vs vertical (un host, muchos puertos: interés en un objetivo).
2. Externo: comprobar si el perímetro lo bloqueó y si hay servicios expuestos que respondieron. El escaneo externo es ruido constante; el valor está en lo que respondió.
3. **Interno**: prioridad máxima en identificar el origen. Un equipo de usuario escaneando la red casi nunca es legítimo → revisar el host origen con EDR (proceso responsable, quién está conectado, malware).
4. Cruzar con la lista de escáneres autorizados (vulnerability scanners, monitorización, pentest en curso).
5. Buscar la fase siguiente: intentos de login, explotación o conexiones establecidas hacia los hosts descubiertos tras el escaneo.
6. Si hay enumeración de AD: revisar qué cuenta la hizo y desde dónde.

---

## Evidencias

| Timestamp (UTC) | Origen | Destino(s) | Puerto(s) | Protocolo | Resultado | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿El escaneo estaba autorizado (escáner corporativo, pentest con ventana)?
- ¿El origen es un servidor de seguridad conocido o un equipo de usuario?
- ¿Qué respondió al escaneo? ¿Afecta a activos críticos?
- ¿Hubo explotación, login o conexión posterior a los hosts descubiertos?
- ¿El origen interno podría estar comprometido? ¿Qué proceso escanea?
- ¿Hay más alertas desde la misma IP en otros sensores?

## Falsos positivos habituales

- Escáneres de vulnerabilidades corporativos y herramientas de inventario/monitorización (mantener lista blanca documentada).
- Software legítimo con discovery (impresión, VoIP, backup, DHCP/mDNS).
- Pentest o red team autorizado (verificar ventana y alcance).
- Balanceadores y health-checks.

---

## Contención recomendada (si se confirma origen comprometido)

- [ ] Aislar host origen interno
- [ ] Bloquear IP externa en perímetro
- [ ] Investigar el host origen como caso de compromiso (malware/persistencia)
- [ ] Vigilar los hosts que respondieron al escaneo

## Observables a extraer (TheHive)

ip (origen), hostname (origen interno), other (herramienta identificada).

---

## Veredicto

- [ ] Escaneo autorizado
- [ ] Ruido externo bloqueado
- [ ] Reconocimiento sospechoso
- [ ] Host interno comprometido (→ nuevo caso sobre el origen)
- [ ] Falso positivo (software con discovery)
