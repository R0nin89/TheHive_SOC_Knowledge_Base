# Cambios sensibles de identidad

## Objetivo

Investigar creación, eliminación, habilitación o modificación de cuentas, resets de contraseña y cambios de privilegios, y validar si están autorizados.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0003 Persistence | T1136 Create Account, T1098 Account Manipulation |
| TA0004 Privilege Escalation | T1078 Valid Accounts |
| TA0005 Defense Evasion | T1531 Account Access Removal (si se eliminan cuentas legítimas) |

## Severidad orientativa

- **Medium**: cambio sin ticket sobre cuenta estándar.
- **High**: reset o cambio sobre cuenta privilegiada sin autorización, cuenta creada fuera de proceso.
- **Critical**: creación de cuenta + alta en grupo privilegiado, o cadena reset → login → cambios.

## Fuentes de datos

- Windows/AD: 4720 (creación), 4722 (habilitación), 4723/4724 (cambio/reset de contraseña), 4725 (deshabilitación), 4726 (eliminación), 4738 (modificación), 4740/4767 (bloqueo/desbloqueo).
- Identidad cloud: audit logs (usuarios, roles, MFA, aplicaciones).
- Sistema de ticketing (para validar autorización).

---

## Datos del cambio

| Campo | Valor |
|---|---|
| Usuario objetivo | |
| Usuario ejecutor | |
| Objeto afectado (atributo, credencial, rol) | |
| Acción | |
| Host / herramienta origen del cambio | |
| Ticket / cambio autorizado | |
| Timestamp (UTC) | |

---

## Pasos de investigación

1. Identificar ejecutor real: si el cambio lo hizo una cuenta de servicio o herramienta IAM, ¿quién lo pidió aguas arriba?
2. Validar autorización: ticket, aprobación, ventana de cambio. "Suele hacerlo él" no es autorización.
3. Analizar la cadena temporal: ¿qué hizo el ejecutor antes (login anómalo, escalada) y qué hizo la cuenta objetivo después (login, accesos)?
4. Para resets: ¿el reset lo pidió el usuario por el canal oficial (helpdesk verificado)? El vishing al helpdesk es un vector común.
5. Para cuentas nuevas: nombre similar a cuentas legítimas (typosquatting interno), descripción vacía, sin asignación a empleado real.
6. Comprobar cambios acompañantes: MFA, grupos, SPNs, delegaciones.

---

## Evidencias

| Timestamp (UTC) | Acción | Usuario objetivo | Ejecutor | Objeto | Origen | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿Existe ticket o autorización que cubra exactamente este cambio?
- ¿El ejecutor es el esperado para este tipo de cambio (rol, equipo, herramienta)?
- ¿La cuenta objetivo es privilegiada o de servicio?
- ¿El cambio ocurrió fuera de horario o desde un host inusual?
- ¿Hubo login de la cuenta objetivo tras el cambio? ¿Desde dónde?
- ¿El propio ejecutor muestra señales de compromiso?
- ¿Debe revertirse el cambio de inmediato?

## Falsos positivos habituales

- Provisioning/deprovisioning automatizado (IAM, RRHH sync): validar la fuente aguas arriba.
- Helpdesk realizando resets legítimos con ticket.
- Cambios masivos por caducidad de política.

---

## Contención recomendada (si se confirma)

- [ ] Revertir el cambio (deshabilitar cuenta creada, restaurar privilegios)
- [ ] Revocar sesiones y resetear la cuenta objetivo y, si procede, la del ejecutor
- [ ] Revisar toda la actividad del ejecutor comprometido
- [ ] Reforzar el proceso de verificación del helpdesk si fue ingeniería social

## Observables a extraer (TheHive)

other (cuentas implicadas), hostname (origen del cambio), ip.

---

## Veredicto

- [ ] Cambio autorizado
- [ ] Cambio sin autorización (error de proceso)
- [ ] Cambio malicioso / escalada de privilegios
- [ ] Persistencia del atacante
- [ ] Falso positivo
