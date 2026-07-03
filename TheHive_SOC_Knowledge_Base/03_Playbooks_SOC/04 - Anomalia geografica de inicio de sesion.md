# Anomalía geográfica de inicio de sesión

## Objetivo

Investigar accesos desde ubicaciones geográficas anómalas, incompatibles entre sí ("viaje imposible") o no habituales para una cuenta.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0001 Initial Access | T1078 Valid Accounts |

## Severidad orientativa

- **Low/Medium**: anomalía aislada, sin login exitoso o explicable (VPN, viaje).
- **High**: viaje imposible con login exitoso, o anomalía + actividad sensible posterior.
- Escalar al playbook `03 - Sospecha de toma de cuenta.md` si se confirma acceso ilegítimo.

## Fuentes de datos

- Sign-in logs con geolocalización, ASN, dispositivo y user-agent.
- Registros de VPN corporativa (para descartar que la "anomalía" sea la salida de la VPN).
- RRHH / calendario del usuario (viajes) si el proceso lo permite.

---

## Datos

| Campo | Valor |
|---|---|
| Usuario | |
| Ubicación habitual (línea base 30 días) | |
| Nueva ubicación | |
| IP origen | |
| ASN / proveedor (¿hosting, VPN, móvil?) | |
| Dispositivo / user-agent | |
| Servicio | |
| Login correcto | |
| MFA superado | |
| Distancia/tiempo entre logins (si viaje imposible) | |

---

## Pasos de investigación

1. Verificar la calidad del dato: la geolocalización por IP es imprecisa, sobre todo en móviles y VPNs. Identificar el **ASN** antes que el país.
2. Comparar contra línea base del usuario (ubicaciones, dispositivos, horarios de 30 días).
3. Si es "viaje imposible": comprobar que ambos logins son reales y no uno de una app en background con IP de datacenter.
4. Comprobar si el dispositivo/user-agent del acceso anómalo coincide con los habituales del usuario (dispositivo conocido + país nuevo suele ser viaje/VPN; dispositivo nuevo + país nuevo es más sospechoso).
5. Revisar actividad posterior al login anómalo (correo, MFA, reglas, datos).
6. Si procede, contactar con el usuario por un canal verificado (no responder al correo posiblemente comprometido).

---

## Evidencias geográficas

| Timestamp (UTC) | Usuario | IP | País / Ciudad | ASN | Dispositivo | Resultado |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿La ubicación es realmente anómala contra la línea base o solo "distinta"?
- ¿Puede explicarse por VPN, proxy, roaming, IP móvil o proveedor cloud?
- ¿Hay dos ubicaciones incompatibles temporalmente con logins interactivos reales?
- ¿El dispositivo es conocido?
- ¿Hubo actividad posterior sensible?
- ¿La cuenta es privilegiada?
- ¿Debe revocarse la sesión de forma preventiva?

## Falsos positivos habituales

- VPNs personales/corporativas y proxies (causa nº 1).
- IPs de operadores móviles geolocalizadas en otra región o país.
- Apps en segundo plano autenticando desde datacenters.
- Viajes reales del usuario.

---

## Contención recomendada (si se confirma)

- [ ] Revocar sesiones
- [ ] Reset de contraseña + revisión MFA
- [ ] Continuar con el playbook 03 (toma de cuenta)

## Observables a extraer (TheHive)

ip, user-agent, other (ASN).

---

## Veredicto

- [ ] Anomalía explicada (viaje / dispositivo legítimo)
- [ ] Uso de VPN/proxy autorizado
- [ ] Toma de cuenta sospechosa (vigilancia)
- [ ] Toma de cuenta confirmada (→ playbook 03)
- [ ] Falso positivo (dato de geolocalización erróneo)
