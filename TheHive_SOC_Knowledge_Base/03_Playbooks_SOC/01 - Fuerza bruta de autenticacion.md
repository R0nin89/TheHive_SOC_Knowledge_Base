# Fuerza bruta de autenticación

## Objetivo

Investigar múltiples intentos fallidos de autenticación contra una o varias cuentas y determinar si hubo acceso exitoso.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0006 Credential Access | T1110 Brute Force (T1110.001 Password Guessing, T1110.002 Password Cracking) |

## Severidad orientativa

- **Medium**: fallos sin login exitoso, cuenta estándar, origen bloqueado.
- **High**: login exitoso posterior, cuenta privilegiada, o campaña desde múltiples orígenes.
- **Critical**: login exitoso en cuenta privilegiada o actividad posterior sospechosa.

## Fuentes de datos

- Windows: Event ID 4625 (fallos), 4624 (éxito), 4740 (bloqueo), 4767 (desbloqueo).
- Identidad cloud (Entra ID / Okta / Google): logs de sign-in, códigos de error de autenticación.
- VPN / correo / aplicaciones expuestas: logs de autenticación propios.
- Linux SSH: ver playbook `14 - Fuerza bruta SSH Linux.md`.

---

## Datos iniciales

- Usuario(s) afectado(s):
- IP(s) origen (con ASN / país / reputación):
- Servicio afectado (VPN, OWA, RDP, SSO, aplicación):
- Número de fallos y ritmo (fallos/minuto):
- ¿Hubo login correcto posterior?:
- Ventana temporal (UTC):
- ¿Cuenta privilegiada o de servicio?:
- Origen interno / externo:
- ¿MFA habilitado en la cuenta?:

---

## Pasos de investigación

1. Cuantificar: nº de fallos, nº de cuentas, nº de orígenes, ventana temporal.
2. Distinguir patrón: 1 cuenta / muchos intentos = fuerza bruta; muchas cuentas / pocos intentos = password spraying (usar playbook 02).
3. Buscar el evento clave: **login exitoso desde el mismo origen** durante o después de los fallos.
4. Si hubo éxito: revisar actividad posterior (cambios MFA, reglas de buzón, accesos a datos, lateralidad) → considerar playbook `03 - Sospecha de toma de cuenta.md`.
5. Enriquecer la IP origen (reputación, ASN, ¿VPN/proxy/Tor?).
6. Ampliar: ¿la misma IP ataca otras cuentas o servicios? ¿Otras IPs atacan la misma cuenta?
7. Revisar si el usuario reconoce la actividad (error propio, cambio de contraseña reciente, dispositivo con credenciales caducadas).

---

## Evidencias

| Timestamp (UTC) | Usuario | IP origen | Servicio | Resultado | Código de error | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas de triaje

- ¿Los fallos afectan a una sola cuenta o a varias?
- ¿Existe login correcto después de los fallos? ¿Desde el mismo origen?
- ¿La cuenta es privilegiada o de servicio?
- ¿El origen es conocido (oficina, VPN corporativa, rango del usuario)?
- ¿El patrón es manual (irregular) o automatizado (ritmo constante)?
- ¿Hay bloqueos de cuenta (4740)? ¿Se desbloqueó alguien la cuenta después?
- ¿Hay cambios posteriores de contraseña, MFA o privilegios?
- ¿MFA detuvo el acceso aunque la contraseña fuera correcta? (buscar fallos "MFA required/denied")

## Falsos positivos habituales

- Credenciales caducadas guardadas en dispositivos, clientes de correo o scripts (patrón: mismo origen interno, mismo usuario, ritmo regular, sin variación).
- Cuentas de servicio tras un cambio de contraseña.
- Escáneres de vulnerabilidades o herramientas de monitorización internas.
- Usuario que olvidó su contraseña (pocos intentos, luego reset legítimo por helpdesk).

---

## Contención recomendada (si se confirma)

- [ ] Bloquear IP origen (si no es infraestructura compartida)
- [ ] Forzar reset de contraseña + revocar sesiones (en este orden inverso: primero revocar)
- [ ] Verificar / exigir MFA
- [ ] Revisar actividad de la cuenta si hubo login exitoso
- [ ] Valorar geo-bloqueo o hardening del servicio expuesto

## Observables a extraer (TheHive)

ip (origen), other (usuario objetivo), hostname (servicio/host destino), user-agent si está disponible.

---

## Veredicto

- [ ] Fuerza bruta fallida (sin acceso)
- [ ] Fuerza bruta exitosa (acceso confirmado → escalar)
- [ ] Password spraying (reclasificar al playbook 02)
- [ ] Error legítimo / credencial caducada
- [ ] Falso positivo
