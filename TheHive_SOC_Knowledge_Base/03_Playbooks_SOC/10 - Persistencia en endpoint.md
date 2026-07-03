# Persistencia en endpoint

## Objetivo

Investigar creación o modificación de mecanismos de persistencia y determinar qué ejecutan, quién los creó y si son maliciosos.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0003 Persistence | T1543.003 Windows Service|
||T1053.005 Scheduled Task|
||T1547.001 Registry Run Keys / Startup Folder|
||T1053.003 Cron, T1543.002 Systemd Service|
||T1098.004 SSH Authorized Keys
||T1546.003 WMI Event Subscription |

## Severidad orientativa

- **Medium**: mecanismo nuevo sin justificar, payload aún no analizado.
- **High**: la persistencia ejecuta un binario/script sospechoso o se creó tras actividad anómala.
- **Critical**: persistencia de malware confirmado o presente en múltiples hosts.

## Fuentes de datos

- Windows: 7045 (servicio nuevo, log System), 4697 (servicio, Security), 4698/4699/4702 (tareas programadas), Sysmon EID 12/13 (registro), 1 (proceso creador).
- Linux: auditd (cambios en `/etc/cron*`, `/etc/systemd/system`, `~/.ssh/authorized_keys`), journal.
- EDR: autoruns / inventario de persistencia.

---

## Mecanismos

- [ ] Servicio
- [ ] Tarea programada
- [ ] Clave de registro (Run/RunOnce/Winlogon/IFEO)
- [ ] Carpeta de inicio
- [ ] WMI event subscription
- [ ] Cron
- [ ] Systemd (service/timer)
- [ ] Claves SSH (`authorized_keys`)
- [ ] Shell profile (`.bashrc`, `.profile`)
- [ ] Extensión/plugin de aplicación
- [ ] Otro:

---

## Datos

| Campo | Valor |
|---|---|
| Host | |
| Usuario que lo creó | |
| Proceso que lo creó | |
| Mecanismo | |
| Ruta / nombre | |
| Qué ejecuta (CommandLine / binario destino) | |
| Hash y firma del binario/script ejecutado | |
| Timestamp de creación (UTC) | |

---

## Pasos de investigación

1. Identificar **qué ejecuta** la persistencia: binario, script, argumentos, ruta (¿carpeta de usuario/temp = sospechoso?).
2. Analizar el payload: hash, firma, reputación, y si es script, su contenido.
3. Identificar **quién y qué la creó**: proceso creador y su árbol (una tarea creada por un proceso de Office es red flag).
4. Reconstruir el contexto previo: ¿qué pasó en el host antes de la creación (descarga, phishing, RDP, exploit)?
5. Comprobar si ya se ha ejecutado y qué hizo (procesos hijos, red).
6. Buscar el mismo mecanismo/nombre/hash en el resto del parque.
7. Nombres engañosos: persistencias que imitan servicios legítimos (GoogleUpdate, OneDrive...) con ruta o firma incorrecta.

---

## Preguntas

- ¿El mecanismo está autorizado o lo instala software conocido?
- ¿Qué ejecuta exactamente y desde qué ruta?
- ¿El binario/script está firmado y tiene buena reputación?
- ¿Quién/qué proceso lo creó y en qué contexto?
- ¿Persiste tras reinicio? ¿Se recrea al eliminarlo (proceso guardián)?
- ¿Está presente en más hosts?
- ¿Debe eliminarse ya o vigilarse (PAP)?

## Falsos positivos habituales

- Instalación/actualización de software legítimo (crea servicios y tareas constantemente).
- Agentes corporativos (EDR, inventario, backup).
- Tareas de mantenimiento del propio SO.

> Truco: la persistencia legítima suele apuntar a rutas de `Program Files`/`/usr` con binarios firmados; la maliciosa suele apuntar a rutas de usuario, temp o scripts.

---

## Contención recomendada (si se confirma)

- [ ] Deshabilitar (no borrar aún) la persistencia y preservar el payload como evidencia
- [ ] Matar procesos asociados / aislar host
- [ ] Bloquear hash
- [ ] Eliminar la persistencia y validar que no se recrea
- [ ] Buscar y limpiar el resto de hosts

## Observables a extraer (TheHive)

hash, filename, registry (clave), other (nombre de tarea/servicio), domain/ip si contacta red.

---

## Veredicto

- [ ] Persistencia legítima (software/agente identificado)
- [ ] Persistencia sospechosa sin confirmar
- [ ] Persistencia maliciosa confirmada
- [ ] Falso positivo
