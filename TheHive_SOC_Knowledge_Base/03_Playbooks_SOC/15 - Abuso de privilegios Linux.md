# Abuso de privilegios Linux

## Objetivo

Investigar uso anómalo de sudo, su, root login o cambios en ficheros críticos.

---

## Datos

| Campo | Valor |
|---|---|
| Host | |
| Usuario | |
| Comando | |
| Ruta modificada | |
| Resultado | |
| Timestamp | |

---

## Ficheros críticos

| Ruta | Riesgo |
|---|---|
| /etc/passwd | Usuarios |
| /etc/shadow | Contraseñas |
| /etc/sudoers | Privilegios |
| sshd_config | Acceso remoto |
| authorized_keys | Persistencia |
| cron / systemd | Persistencia |

---

## Preguntas

- ¿El usuario debía usar privilegios?
- ¿Qué comando ejecutó?
- ¿Se modificaron ficheros críticos?
- ¿Hay persistencia?
- ¿Hubo login remoto previo?
- ¿Existe autorización?

---

## Veredicto

- [ ] Administración legítima
- [ ] Abuso de privilegios
- [ ] Persistencia
- [ ] Falso positivo
