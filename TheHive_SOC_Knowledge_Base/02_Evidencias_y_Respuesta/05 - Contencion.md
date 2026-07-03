# Contención

> Antes de contener: valorar si la contención alerta al atacante (PAP) y si hay que **preservar evidencias primero** (volcado de memoria, triage del disco, exportación de logs). En casos con posible acción legal, priorizar cadena de custodia.

## Preparación

- ¿Evidencias volátiles preservadas antes de actuar? (memoria, conexiones activas, procesos):
- ¿Aprobación necesaria? (propietario del activo, responsable de turno):
- ¿Riesgo de impacto en negocio al contener? (servicio crítico, producción):

---

## Acciones de contención

| Acción | Activo / Usuario | Responsable | Fecha/hora (UTC) | Resultado | Reversible |
|---|---|---|---|---|---|
| Bloquear IP | | | | | Sí |
| Bloquear dominio / URL | | | | | Sí |
| Bloquear hash | | | | | Sí |
| Resetear contraseña | | | | | — |
| Revocar sesiones / tokens (incluir refresh tokens y OAuth) | | | | | — |
| Deshabilitar cuenta | | | | | Sí |
| Aislar host (network containment EDR) | | | | | Sí |
| Detener proceso / cuarentena de fichero | | | | | Parcial |
| Eliminar persistencia (servicio, tarea, cron, clave) | | | | | — |
| Retirar privilegios / sacar de grupo | | | | | Sí |
| Deshabilitar regla de buzón / reenvío | | | | | Sí |

> Orden recomendado ante cuenta comprometida: 1) revocar sesiones, 2) resetear contraseña, 3) revisar métodos MFA registrados, 4) revisar reglas de buzón y aplicaciones OAuth consentidas. Resetear sin revocar sesiones deja al atacante dentro.

---

## Riesgo residual

- ¿Queda acceso activo (sesiones, tokens, VPN, claves SSH)?:
- ¿Queda persistencia sin eliminar?:
- ¿Quedan IOCs sin bloquear?:
- ¿Hay sistemas sin revisar dentro del alcance?:
- ¿Hay usuarios sin notificar?:
- ¿Puede el atacante volver por el mismo vector (vulnerabilidad sin parchear, credencial filtrada)?:

---

## Validación de contención

| Prueba | Resultado | Evidencia |
|---|---|---|
| El IOC bloqueado ya no genera tráfico/eventos | | |
| La cuenta no registra nuevos logins | | |
| El host aislado no tiene conexiones salientes | | |
| No reaparece la persistencia tras reinicio | | |
