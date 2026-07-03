# Password spraying

## Objetivo

Investigar una IP o conjunto de IPs intentando autenticarse contra muchos usuarios con pocos intentos por cuenta (para evadir bloqueos por umbral).

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0006 Credential Access | T1110.003 Password Spraying |
| TA0043 Reconnaissance | T1589.002 Email Addresses (enumeración previa de usuarios) |

## Severidad orientativa

- **Medium**: spraying sin ningún login exitoso.
- **High**: cualquier login exitoso, o cuentas privilegiadas entre los objetivos.
- **Critical**: login exitoso + actividad posterior (reglas de buzón, MFA nuevo, acceso a datos).

## Fuentes de datos

- Windows: 4625 agregados por IP origen; 4771/4776 en DC (Kerberos/NTLM).
- Identidad cloud: sign-in logs agregados por IP y por aplicación; atención a **legacy auth** (IMAP/POP/SMTP), objetivo habitual del spraying por no soportar MFA.
- VPN / OWA / servicios expuestos.

---

## Indicadores

- Nº de usuarios afectados:
- Intentos por usuario (típico: 1-3):
- IP(s) origen (¿rotan? ¿mismo ASN/proveedor?):
- Servicio / protocolo atacado (¿legacy auth?):
- ¿Login correcto en alguna cuenta?:
- Cuentas bloqueadas:
- ¿Los usuarios objetivo siguen orden alfabético o patrón de directorio? (indica lista enumerada)

---

## Pasos de investigación

1. Agregar fallos por IP origen: nº usuarios distintos, intentos por usuario, ventana.
2. Confirmar el patrón spraying: muchos usuarios, pocos intentos, a menudo espaciados en el tiempo (low & slow).
3. Buscar **cualquier 4624 / sign-in exitoso** desde las IPs implicadas: es la prioridad absoluta.
4. Identificar si los usuarios objetivo existen todos (lista filtrada/enumerada) o hay muchos inexistentes (lista genérica).
5. Comprobar si el ataque usa legacy auth o endpoints sin MFA.
6. Enriquecer IPs (ASN, país, ¿hosting/VPN/proxy residencial?) y buscar IPs "hermanas" del mismo rango.
7. Para cuentas con login exitoso: pivotar al playbook `03 - Sospecha de toma de cuenta.md`.

---

## Usuarios afectados

| Usuario | Nº fallos | ¿Bloqueado? | ¿Login correcto? | ¿Privilegiado? | Observación |
|---|---:|---|---|---|---|
| | | | | | |

## Orígenes

| IP origen | Nº usuarios | ASN / País | Tipo (hosting/VPN/residencial) | Reputación | Acción |
|---|---:|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿El origen intenta contra muchos usuarios con pocos intentos por cuenta?
- ¿Hay cuentas privilegiadas o VIP entre los objetivos?
- ¿Hubo algún login correcto? ¿Con o sin MFA superado?
- ¿Coincide con una filtración de credenciales reciente de la organización?
- ¿El ataque continúa en este momento?
- ¿Se requiere reset masivo, bloqueo selectivo o bloqueo de protocolo legacy?

## Falsos positivos habituales

- Gateways / proxies internos que concentran la autenticación de muchos usuarios tras una misma IP (los fallos de muchos usuarios desde 1 IP interna pueden ser normales).
- Sincronizaciones masivas tras caducidad de política de contraseñas.
- Herramientas de auditoría de contraseñas autorizadas.

---

## Contención recomendada (si se confirma)

- [ ] Bloquear IP(s) origen
- [ ] Revocar sesiones + reset de las cuentas con login exitoso
- [ ] Deshabilitar legacy auth si fue el vector
- [ ] Notificar a los usuarios objetivo (sin desvelar más de lo necesario)
- [ ] Reforzar MFA / acceso condicional

## Observables a extraer (TheHive)

ip (todas las de origen), other (lista de usuarios objetivo, como fichero adjunto si son muchos), user-agent.

---

## Veredicto

- [ ] Password spraying confirmado sin acceso
- [ ] Password spraying con acceso (→ toma de cuenta, escalar)
- [ ] Sospecha no confirmada
- [ ] Actividad legítima / infraestructura interna
- [ ] Falso positivo
