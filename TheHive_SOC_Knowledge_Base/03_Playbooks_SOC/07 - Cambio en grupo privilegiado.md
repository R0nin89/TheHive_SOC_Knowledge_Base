# Cambio en grupo privilegiado

## Objetivo

Investigar altas o bajas en grupos con privilegios administrativos o acceso sensible (Domain Admins, Enterprise Admins, administradores locales, roles cloud).

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0004 Privilege Escalation | T1078.002 Domain Accounts|
||T1098 Account Manipulation |
| TA0003 Persistence | T1136 Create Account (si se creó la cuenta añadida) |

## Severidad orientativa

- **High** por defecto si no hay ticket.
- **Critical**: alta en grupo de administración de dominio/tenant sin autorización, o cuenta recién creada añadida a grupo privilegiado.

## Fuentes de datos

- Windows/AD: 4728 (grupo global), 4732 (grupo local), 4756 (grupo universal), 4729/4733/4757 (bajas), 4735 (grupo modificado).
- Identidad cloud: asignaciones de rol (audit log), activaciones PIM/JIT.
- Sistema de ticketing.

---

## Datos

- Grupo afectado y privilegios que otorga:
- Usuario añadido / eliminado (¿cuenta nueva? ¿de servicio?):
- Usuario ejecutor:
- Herramienta / host origen del cambio:
- Ticket:
- Timestamp (UTC):
- ¿El cambio sigue vigente ahora mismo?:

---

## Pasos de investigación

1. Determinar el privilegio real que otorga el grupo (algunos grupos "menores" permiten escalar: Backup Operators, DNSAdmins, Account Operators, roles cloud con permisos de escritura en identidad).
2. Validar autorización exacta (ticket, aprobación PIM/JIT, ventana temporal).
3. Investigar la cuenta añadida: antigüedad, propietario, ¿reset o creación reciente?, actividad posterior con el nuevo privilegio (4672, logins en DCs, cambios).
4. Investigar al ejecutor: ¿su sesión muestra señales de compromiso previo?
5. Comprobar si el alta fue transitoria (añadir → actuar → quitar), patrón típico de atacante para no dejar rastro estático.
6. Revisar otros cambios de identidad en la misma ventana.

---

## Evidencias

| Timestamp (UTC) | Acción | Grupo | Usuario afectado | Ejecutor | Origen | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿El grupo otorga privilegios administrativos o acceso a datos sensibles?
- ¿Existe aprobación (ticket / PIM)?
- ¿La cuenta añadida es nueva o tuvo reset reciente?
- ¿Hubo login o acciones con el nuevo privilegio?
- ¿El alta fue temporal y ya se retiró (posible ocultación)?
- ¿Debe retirarse el privilegio de inmediato?

## Falsos positivos habituales

- Activaciones JIT/PIM legítimas (elevación temporal aprobada).
- Automatismos de IAM / onboarding.
- Anidamiento de grupos: el "alta" es consecuencia de otro cambio legítimo.

---

## Contención recomendada (si se confirma)

- [ ] Retirar del grupo inmediatamente
- [ ] Revocar sesiones de la cuenta añadida (los tokens pueden conservar el privilegio)
- [ ] Resetear cuenta añadida y ejecutor si hay compromiso
- [ ] Auditar acciones realizadas con el privilegio durante la ventana
- [ ] Revisar el resto de miembros del grupo

## Observables a extraer (TheHive)

other (grupo, cuentas), hostname (origen), ip.

---

## Veredicto

- [ ] Cambio autorizado (ticket/PIM validado)
- [ ] Escalada de privilegios maliciosa
- [ ] Error de proceso (sin malicia, corregir)
- [ ] Falso positivo (anidamiento / automatismo)
