# Evasión defensiva o borrado de logs

## Objetivo

Investigar borrado de logs, cambios de auditoría o manipulación de controles de seguridad. Premisa: **nadie borra logs sin motivo**; la pregunta central es qué se intentaba ocultar.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0005 Defense Evasion | T1070.001 Clear Windows Event Logs, T1070.002 Clear Linux Logs, T1562.001 Disable or Modify Tools, T1562.002 Disable Windows Event Logging, T1562.004 Disable or Modify System Firewall |

## Severidad orientativa

- **High** por defecto sin justificación inmediata.
- **Critical**: borrado en servidor/DC, desactivación de EDR, o combinado con otra actividad sospechosa.

## Fuentes de datos

- Windows: 1102 (Security log borrado), 104 (log de sistema borrado), 4719 (política de auditoría cambiada), 4688 (`wevtutil cl`, `Clear-EventLog`).
- EDR: consola central (tamper protection, agente desconectado, exclusiones nuevas) — el propio EDR suele conservar telemetría aunque borren logs locales.
- SIEM: los eventos **ya enviados** antes del borrado siguen disponibles: esa es la principal ventaja del analista.
- Linux: auditd, journal, mtime de `/var/log/*`, `history -c` / `.bash_history` truncado.

---

## Datos

| Campo | Valor |
|---|---|
| Host | |
| Usuario ejecutor | |
| Control afectado (log, AV/EDR, firewall, auditoría) | |
| Acción (borrado, desactivación, exclusión, detención de servicio) | |
| Proceso/comando que lo ejecutó | |
| Timestamp (UTC) | |

---

## Pasos de investigación

1. Confirmar la acción y su método (comando, GUI, API) y quién la ejecutó realmente.
2. **Reconstruir la ventana previa con el SIEM/EDR central** (los datos ya exportados sobreviven al borrado local): 30-60 min antes como mínimo, idealmente 24 h.
3. Buscar la actividad que motivó la limpieza: acceso remoto, malware, escalada, movimiento lateral, herramienta ofensiva.
4. Revisar otros signos de evasión en el mismo host: exclusiones AV nuevas, servicios de seguridad detenidos, firewall modificado, timestomping.
5. Comprobar si hay más hosts con la misma acción (script de limpieza del atacante).
6. Validar contra mantenimiento: ¿ticket, ventana de cambio, herramienta de gestión que rota logs?

---

## Timeline previo

| Timestamp (UTC) | Fuente | Evento | Usuario | Observación |
|---|---|---|---|---|
| | | | | |

---

## Preguntas

- ¿Quién realizó la acción y desde qué proceso/sesión?
- ¿Existe mantenimiento autorizado que lo explique?
- ¿Qué ocurrió en el host los 30-60 minutos (y 24 h) anteriores?
- ¿Hay malware, PowerShell sospechoso o acceso remoto previo?
- ¿Se desactivaron otros controles a la vez?
- ¿El SIEM tiene los eventos previos al borrado?
- ¿Se debe aislar el host?

## Falsos positivos habituales

- Rotación/limpieza de logs por herramientas de gestión o scripts programados (patrón: mismo horario, muchos hosts, misma herramienta).
- Reinstalaciones/reprovisionado de equipos.
- Administradores liberando espacio en disco (mala práctica; documentar y corregir).

---

## Contención recomendada (si se confirma)

- [ ] Aislar host
- [ ] Deshabilitar cuenta ejecutora y revocar sesiones
- [ ] Restaurar controles (reactivar EDR/auditoría, quitar exclusiones)
- [ ] Preservar evidencias restantes (memoria, artefactos forenses) antes de tocar más
- [ ] Escalar: la evasión confirmada implica un atacante con acceso, tratar como incidente

## Observables a extraer (TheHive)

hostname, other (usuario, comando), hash (herramienta usada si existe).

---

## Veredicto

- [ ] Mantenimiento autorizado
- [ ] Evasión defensiva confirmada (→ incidente)
- [ ] Mala práctica administrativa (sin malicia)
- [ ] Falso positivo
