# Fuerza bruta SSH Linux

## Objetivo

Investigar múltiples intentos fallidos SSH y comprobar si hubo acceso exitoso posterior.

---

## Datos

| Campo | Valor |
|---|---|
| Host | |
| Usuario objetivo | |
| IP origen | |
| Nº fallos | |
| Login exitoso | |
| Método | |
| Timestamp inicial | |
| Timestamp final | |

---

## Logs

| Timestamp | Usuario | IP origen | Resultado | Host |
|---|---|---|---|---|
| | | | | |

---

## Preguntas

- ¿Hubo login exitoso después?
- ¿El usuario era root o sudoer?
- ¿El origen es conocido?
- ¿Hay escaneo previo?
- ¿Hay comandos sospechosos después del login?
- ¿Hay cambios en claves SSH?

---

## Contención

- [ ] Bloquear IP
- [ ] Revisar permisos SSH
- [ ] Rotar credenciales
- [ ] Revisar usuarios privilegiados
- [ ] Revisar claves autorizadas
