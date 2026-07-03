# Abuso de privilegios Linux

## Objetivo

Investigar uso anómalo de sudo, su, login de root o cambios en ficheros críticos del sistema.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0004 Privilege Escalation | T1548.003 Sudo and Sudo Caching|
|| T1068 Exploitation for Privilege Escalation |
| TA0003 Persistence | T1098.004 SSH Authorized Keys|
||T1053.003 Cron, T1136.001 Local Account |
| TA0005 Defense Evasion | T1070.002 Clear Linux Logs|
|| T1222.002 File Permission Modification |

## Severidad orientativa

- **Medium**: uso anómalo de sudo por usuario legítimo, sin cambios críticos.
- **High**: modificación de sudoers/shadow/authorized_keys sin autorización, o escalada desde cuenta no privilegiada.
- **Critical**: escalada confirmada + persistencia o borrado de logs.

## Fuentes de datos

- `/var/log/auth.log` o `/var/log/secure`: sudo (comando incluido), su, sesiones.
- auditd: reglas sobre ficheros críticos (syscalls write/attr), execve.
- `.bash_history` de usuario y root, EDR Linux.
- Integridad de ficheros (AIDE/OSSEC) si existe.

## Ficheros críticos y su riesgo

| Ruta | Riesgo |
|---|---|
| /etc/passwd, /etc/shadow | Usuarios y contraseñas (usuario nuevo con UID 0 = backdoor) |
| /etc/sudoers, /etc/sudoers.d/ | Privilegios (NOPASSWD nuevo = escalada persistente) |
| /etc/ssh/sshd_config | Acceso remoto (PermitRootLogin, puertos) |
| ~/.ssh/authorized_keys | Persistencia de acceso |
| /etc/cron*, crontabs, systemd units | Persistencia de ejecución |
| /etc/ld.so.preload, LD_PRELOAD | Inyección/rootkit userland |
| Binarios con SUID nuevo | Escalada (`find / -perm -4000 -newer <ref>`) |

---

## Datos

| Campo | Valor |
|---|---|
| Host | |
| Usuario (y desde qué sesión/IP venía) | |
| Comando ejecutado | |
| Fichero/ruta modificada | |
| Resultado (éxito/denegado) | |
| Timestamp (UTC) | |

---

## Pasos de investigación

1. Reconstruir la sesión completa del usuario: origen del login (IP, hora), comandos antes y después del evento.
2. Determinar el tipo de acción: administración (esperada por rol) vs escalada (usuario sin privilegios usando exploits, sudo denegado repetido, GTFOBins).
3. Si hay cambios en ficheros críticos: obtener diff (valor anterior/nuevo) y buscar usuarios con UID 0, entradas NOPASSWD, claves nuevas.
4. Buscar señales de exploit local (kernel/sudo CVEs): binarios compilados en /tmp, gcc reciente, crashes.
5. Revisar persistencia y limpieza (history truncado, logs tocados).
6. Validar autorización (ticket, rol del usuario, cambio programado).

---

## Preguntas

- ¿El usuario tiene rol que justifique el privilegio?
- ¿Qué comando ejecutó exactamente y qué modificó?
- ¿Hay entradas nuevas en sudoers, usuarios UID 0 o claves SSH añadidas?
- ¿Hay intentos denegados previos (prueba y error de escalada)?
- ¿Hubo login remoto anómalo previo a la actividad?
- ¿Hay persistencia o borrado de rastro posterior?
- ¿Existe autorización documentada?

## Falsos positivos habituales

- Administradores y DevOps en operación normal (validar por rol y ticket).
- Herramientas de configuración (Ansible, Puppet, Chef) modificando ficheros críticos de forma programada.
- Instaladores de paquetes tocando cron/systemd.

---

## Contención recomendada (si se confirma)

- [ ] Matar sesiones del usuario y deshabilitar la cuenta
- [ ] Revertir cambios en ficheros críticos (con copia previa como evidencia)
- [ ] Eliminar persistencia (claves, cron, usuarios nuevos, SUID)
- [ ] Aislar host; valorar reimagen si hubo root no autorizado
- [ ] Rotar credenciales y secretos accesibles desde el host

## Observables a extraer (TheHive)

other (usuario, comando), hostname, ip (origen de la sesión), hash (binarios/exploits).

---

## Veredicto

- [ ] Administración legítima
- [ ] Abuso de privilegios (usuario legítimo, uso indebido)
- [ ] Escalada de privilegios maliciosa
- [ ] Persistencia establecida
- [ ] Falso positivo
