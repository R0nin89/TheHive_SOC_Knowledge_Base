# Evidencias endpoint

## Procesos

| Timestamp (UTC) | Host | Usuario | Proceso | Proceso padre | CommandLine | Hash (SHA256) |
|---|---|---|---|---|---|---|
| | | | | | | |

> Señales de alerta: procesos de Office/navegador lanzando shells, binarios firmados con argumentos anómalos, ejecuciones desde `%TEMP%`, `%APPDATA%`, `C:\Users\Public`, `/tmp`, `/dev/shm`.

---

## Ficheros

| Timestamp (UTC) | Host | Ruta | Acción (creado/modificado/borrado) | Hash | Usuario |
|---|---|---|---|---|---|
| | | | | | |

---

## Registro / configuración

| Timestamp (UTC) | Host | Clave / Configuración | Valor anterior | Valor nuevo | Usuario |
|---|---|---|---|---|---|
| | | | | | |

> Claves de persistencia habituales: `Run`, `RunOnce`, `Winlogon\Shell`, `Image File Execution Options`, servicios (`HKLM\SYSTEM\CurrentControlSet\Services`).

---

## Seguridad local

| Control | Estado | Evidencia |
|---|---|---|
| Antivirus / EDR (activo, exclusiones nuevas) | | |
| Firewall local | | |
| Auditoría / logging | | |
| Cuentas locales (nuevas, habilitadas) | | |
| Persistencia (servicios, tareas, autoruns, cron, systemd) | | |

---

## Artefactos por sistema operativo

**Windows:** Prefetch, Amcache, Shimcache, tareas programadas, servicios, WMI subscriptions, historial de PowerShell (`ConsoleHost_history.txt`), carpetas de inicio.

**Linux:** `~/.bash_history`, `/var/log/auth.log` o `/var/log/secure`, crontabs (`/etc/cron*`, `crontab -l`), unidades systemd, `authorized_keys`, binarios con SUID recientes, `/etc/passwd` y `/etc/shadow` (mtime).

**macOS:** LaunchAgents/LaunchDaemons, perfiles de configuración, TCC.

---

## Conclusión endpoint

- ¿Hubo ejecución?:
- ¿Hubo persistencia?:
- ¿Hubo malware?:
- ¿Hubo acceso a credenciales (LSASS, SAM, keychain)?:
- ¿Hubo movimiento lateral?:
- ¿Host contenido? (método y hora):
