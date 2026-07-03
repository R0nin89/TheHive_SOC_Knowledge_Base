# Fuerza bruta SSH Linux

## Objetivo

Investigar múltiples intentos fallidos SSH contra hosts Linux y comprobar si hubo acceso exitoso y actividad posterior.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0006 Credential Access | T1110.001 Password Guessing |
| TA0001 Initial Access | T1078 Valid Accounts|
|| T1133 External Remote Services |
| TA0003 Persistence | T1098.004 SSH Authorized Keys |

## Severidad orientativa

- **Low**: ruido de Internet contra host expuesto, sin éxito (constante en cualquier IP pública con el 22 abierto).
- **High**: login exitoso tras fallos, usuario root/sudoer, o host interno atacado desde otro host interno (lateralidad).
- **Critical**: acceso exitoso + comandos post-explotación o persistencia.

## Fuentes de datos

- `/var/log/auth.log` (Debian/Ubuntu) o `/var/log/secure` (RHEL): `Failed password`, `Accepted password/publickey`, `Invalid user`.
- `lastb` (fallos), `last` (accesos), `w`/`who` (sesiones activas).
- auditd / EDR Linux: comandos post-login.
- `~/.ssh/authorized_keys` (mtime y contenido), `~/.bash_history`.
- Firewall/NetFlow: origen y volumen.

---

## Datos

| Campo | Valor |
|---|---|
| Host (¿expuesto a Internet?) | |
| Usuario(s) objetivo (¿existen? ¿root permitido?) | |
| IP origen (ASN, reputación) | |
| Nº fallos y ritmo | |
| Login exitoso (sí/no, hora, método password/key) | |
| Timestamp inicial / final (UTC) | |

---

## Pasos de investigación

1. Cuantificar: fallos por IP, usuarios probados (¿existen o son genéricos: admin, test, oracle?), ventana.
2. Buscar el evento clave: `Accepted password` desde IP atacante durante/después de los fallos.
3. Si hubo acceso: revisar comandos ejecutados (`.bash_history`, auditd, EDR), procesos nuevos, conexiones salientes.
4. Revisar persistencia: claves en `authorized_keys`, cron, systemd, usuarios nuevos (`/etc/passwd`), binarios SUID recientes.
5. Comprobar configuración: `PermitRootLogin`, `PasswordAuthentication`, ¿por qué está expuesto el servicio?
6. Origen interno atacando por SSH = probable host comprometido: abrir caso sobre el origen.
7. Buscar la misma IP contra otros hosts del parque.

---

## Logs

| Timestamp (UTC) | Usuario | IP origen | Resultado | Método | Host |
|---|---|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿Hubo login exitoso después de los fallos? ¿Con contraseña o con clave?
- ¿El usuario era root o sudoer?
- ¿El origen es interno (grave: lateralidad) o ruido externo?
- ¿Hay escaneo previo desde la misma IP?
- ¿Hay comandos sospechosos tras el login (descargas, wget/curl, chmod +x, crontab)?
- ¿Hay cambios en `authorized_keys` o usuarios nuevos?

## Falsos positivos habituales

- Ruido constante de Internet (bots) sin éxito: documentar y valorar hardening, no abrir caso por cada ráfaga.
- Sistemas de despliegue/automatización (Ansible, monitorización) con credenciales caducadas.
- Usuarios legítimos con teclado/keychain desincronizado.

---

## Contención recomendada (si se confirma acceso)

- [ ] Bloquear IP origen; matar sesiones activas (`pkill -u usuario` tras investigar)
- [ ] Rotar credenciales del usuario y revisar sudoers
- [ ] Eliminar claves SSH no autorizadas y persistencia
- [ ] Aislar host si hay post-explotación; valorar reimagen
- [ ] Hardening: deshabilitar password auth y root login, fail2ban, restringir origen (VPN/bastión)

## Observables a extraer (TheHive)

ip (origen), other (usuarios), hash (payloads descargados), domain/url (fuentes de descarga).

---

## Veredicto

- [ ] Fuerza bruta fallida (ruido externo)
- [ ] Fuerza bruta exitosa (→ incidente)
- [ ] Lateralidad interna (→ investigar host origen)
- [ ] Error de automatización legítima
- [ ] Falso positivo
