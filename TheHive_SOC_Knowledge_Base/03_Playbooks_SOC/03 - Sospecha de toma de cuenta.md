# Sospecha de toma de cuenta

## Objetivo

Investigar indicios de compromiso de una cuenta tras autenticación anómala o actividad posterior sospechosa, y determinar qué hizo el atacante con ella.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0001 Initial Access | T1078 Valid Accounts |
| TA0003 Persistence | T1098 Account Manipulation (MFA nuevo, reglas de buzón) |
| TA0009 Collection | T1114 Email Collection |

## Severidad orientativa

- **High** por defecto ante indicios razonables.
- **Critical**: cuenta privilegiada, acceso a datos sensibles, o persistencia establecida (MFA del atacante, OAuth, reglas de reenvío).

## Fuentes de datos

- Sign-in logs (cloud) / 4624-4625 (AD), con IP, geolocalización, dispositivo y user-agent.
- Logs de auditoría de la plataforma (cambios MFA, consentimientos OAuth, reglas de buzón, permisos delegados).
- Logs de acceso a datos (SharePoint/Drive/CRM) y de correo (envíos, reenvíos).

---

## Datos iniciales

- Cuenta afectada y tipo:
- IP origen / ubicación / ASN del acceso sospechoso:
- Dispositivo y user-agent (¿coincide con los habituales?):
- Primer evento sospechoso:
- Actividad posterior detectada:
- ¿Cuenta privilegiada?:
- ¿MFA activo? ¿Método? (SMS y llamada son más débiles que app/FIDO):
- ¿Cómo se sospecha el compromiso? (alerta, aviso del usuario, phishing previo, spraying previo):

---

## Pasos de investigación

1. Construir la línea base de la cuenta: IPs, países, dispositivos y horarios habituales (últimos 30 días).
2. Confirmar el acceso anómalo contra esa línea base (no solo contra la geolocalización).
3. Revisar **persistencia del atacante**, en este orden:
   - Métodos MFA añadidos o cambiados.
   - Reglas de buzón (reenvío externo, mover a RSS/eliminados, borrar avisos de seguridad).
   - Consentimientos OAuth / aplicaciones autorizadas nuevas.
   - Delegaciones de buzón o permisos añadidos.
   - Dispositivos registrados nuevos.
4. Revisar qué se accedió: correo (búsquedas de "password", "factura", "IBAN"), ficheros, sistemas internos.
5. Buscar envíos de correo desde la cuenta (phishing interno / fraude BEC a contactos).
6. Buscar lateralidad: uso de la cuenta contra otros servicios o cuentas.
7. Identificar el vector: phishing previo, spraying, credencial filtrada, MFA fatigue.

---

## Evidencias

| Timestamp (UTC) | Evento | Usuario | IP / Host | Dispositivo/UA | Resultado | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿Hubo login correcto desde origen anómalo respecto a la línea base?
- ¿Hubo fallos o MFA fatigue justo antes del login correcto?
- ¿Se cambiaron contraseña, MFA, reglas de buzón, OAuth o grupos?
- ¿Se accedió a sistemas o datos críticos?
- ¿Se envió correo desde la cuenta (BEC / phishing interno)?
- ¿Hay movimiento lateral o accesos a otras cuentas?
- ¿Hay indicadores de exfiltración?

## Falsos positivos habituales

- VPN personal o corporativa que cambia la geolocalización.
- Viajes, roaming, o IP de operador móvil de otro país.
- Nuevo dispositivo legítimo del usuario.
- Aplicaciones que autentican desde datacenters (sincronización de calendario, apps móviles).

---

## Contención recomendada (si se confirma)

> Orden importante: revocar antes de resetear, y limpiar la persistencia siempre.

- [ ] Revocar todas las sesiones y tokens (incluidos refresh tokens)
- [ ] Reset de contraseña
- [ ] Eliminar métodos MFA no reconocidos y re-registrar MFA con el usuario verificado
- [ ] Eliminar reglas de buzón y consentimientos OAuth maliciosos
- [ ] Deshabilitar cuenta temporalmente si el riesgo es alto
- [ ] Avisar a destinatarios si hubo envíos maliciosos desde la cuenta
- [ ] Revisar actividad histórica completa de la ventana de compromiso

## Observables a extraer (TheHive)

ip (accesos del atacante), mail (direcciones de reenvío), url/domain (phishing origen si se conoce), user-agent, other (app OAuth maliciosa).

---

## Veredicto

- [ ] Toma de cuenta confirmada
- [ ] Toma de cuenta sospechosa no confirmada (vigilancia)
- [ ] Actividad legítima del usuario
- [ ] Falso positivo
