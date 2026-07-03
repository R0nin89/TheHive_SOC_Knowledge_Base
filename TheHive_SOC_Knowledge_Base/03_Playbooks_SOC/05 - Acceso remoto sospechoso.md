# Acceso remoto sospechoso

## Objetivo

Investigar conexiones remotas anómalas (RDP, SSH, VPN, VNC, herramientas de gestión remota), fallidas o exitosas, hacia activos internos.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0001 Initial Access | T1133 External Remote Services |
| TA0008 Lateral Movement | T1021 Remote Services (.001 RDP, .004 SSH, .006 WinRM) |
| TA0011 Command and Control | T1219 Remote Access Software (AnyDesk, TeamViewer, etc.) |

## Severidad orientativa

- **Medium**: acceso anómalo sin confirmación de malicia.
- **High**: acceso exitoso no autorizado, o instalación de herramienta de acceso remoto no aprobada.
- **Critical**: acceso remoto a activo crítico con actividad posterior maliciosa.

## Fuentes de datos

- Windows: 4624 LogonType 10 (RDP) y 3 (red), 4625, logs de TerminalServices (EID 21, 24, 25, 1149).
- Linux: `auth.log`/`secure` (sshd).
- VPN: logs de concentrador (asignación de IP interna incluida).
- EDR: procesos de herramientas RMM (AnyDesk, TeamViewer, ScreenConnect, Atera...), servicios nuevos.
- Firewall: conexiones entrantes a puertos de gestión (3389, 22, 5900...).

---

## Datos

- Usuario:
- IP origen (externa/interna, ASN):
- Host destino y criticidad:
- Servicio remoto (RDP/SSH/VPN/RMM):
- Número de intentos previos:
- Login correcto (sí/no, hora):
- Horario (¿laboral? ¿habitual para ese usuario?):
- Justificación conocida (ticket, mantenimiento):

---

## Pasos de investigación

1. Confirmar el tipo de acceso y su dirección: externo→interno (exposición) o interno→interno (posible lateralidad).
2. Comparar con línea base: ¿ese usuario accede normalmente a ese host, por ese servicio, a esa hora?
3. Si hubo fallos previos y luego éxito: tratar como fuerza bruta exitosa (playbook 01).
4. Revisar la actividad **dentro de la sesión**: procesos ejecutados, ficheros tocados, cuentas usadas (EDR / 4688).
5. Buscar herramientas RMM no aprobadas instaladas o ejecutadas (persistencia habitual de atacantes y de soporte fraudulento).
6. Comprobar accesos en cadena (host A → host B → host C) que indiquen movimiento lateral.
7. Verificar exposición: ¿el servicio debía estar accesible desde ese origen?

---

## Evidencias

| Timestamp (UTC) | Origen | Destino | Usuario | Servicio | Resultado | Actividad en sesión |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿El origen está autorizado para acceder a ese destino?
- ¿El usuario suele acceder remotamente a ese host?
- ¿Hubo fallos antes del acceso correcto?
- ¿El destino es crítico (DC, backup, servidor de negocio)?
- ¿Hay ejecución posterior sospechosa en el host destino?
- ¿Hay herramientas de acceso remoto no corporativas?
- ¿Existe movimiento lateral posterior?

## Falsos positivos habituales

- Administradores y helpdesk en su trabajo habitual (validar con ticket).
- Tareas programadas / herramientas de gestión que abren sesiones de red (LogonType 3) masivamente.
- Escáneres de vulnerabilidades autenticados.
- Teletrabajo desde ubicaciones nuevas.

---

## Contención recomendada (si se confirma)

- [ ] Cerrar la sesión activa / aislar host destino
- [ ] Bloquear IP origen o deshabilitar la cuenta usada
- [ ] Desinstalar / bloquear la herramienta RMM no autorizada
- [ ] Cerrar la exposición (firewall, NLA, VPN obligatoria)
- [ ] Revisar el resto de hosts accesibles con las mismas credenciales

## Observables a extraer (TheHive)

ip (origen), hostname (destino), other (usuario), filename/hash (herramienta RMM si aplica).

---

## Veredicto

- [ ] Acceso autorizado / administración legítima
- [ ] Fuerza bruta remota (→ playbook 01)
- [ ] Movimiento lateral
- [ ] Cuenta comprometida (→ playbook 03)
- [ ] Herramienta de acceso remoto no autorizada
- [ ] Falso positivo
