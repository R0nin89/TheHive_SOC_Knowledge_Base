# Evidencias SIEM

## Alertas relevantes

| Timestamp (UTC) | Activo | Rule ID / Detección | Severidad | Descripción | Usuario | IP origen |
|---|---|---|---:|---|---|---|
| | | | | | | |

---

## Campos clave

| Campo | Valor | Observación |
|---|---|---|
| Usuario origen | | |
| Usuario objetivo | | |
| IP origen | | |
| IP destino | | |
| Host afectado | | |
| Proceso | | |
| Proceso padre | | |
| CommandLine | | |
| Hash (SHA256) | | |
| Event ID | | |
| Dominio / URL | | |
| User-Agent | | |

---

## Event IDs de referencia rápida (Windows)

| Event ID | Fuente | Significado |
|---:|---|---|
| 4624 | Security | Inicio de sesión correcto (ver LogonType: 2 interactivo, 3 red, 10 RDP) |
| 4625 | Security | Inicio de sesión fallido (ver Status/SubStatus) |
| 4648 | Security | Logon con credenciales explícitas (runas, lateralidad) |
| 4672 | Security | Privilegios especiales asignados al iniciar sesión |
| 4688 | Security | Creación de proceso (con línea de comandos si está habilitado) |
| 4720 / 4726 | Security | Cuenta creada / eliminada |
| 4724 / 4723 | Security | Reset de contraseña por tercero / cambio por el propio usuario |
| 4728 / 4732 / 4756 | Security | Alta en grupo global / local / universal |
| 4740 | Security | Cuenta bloqueada |
| 1102 | Security | Log de seguridad borrado |
| 7045 | System | Servicio instalado |
| 4698 | Security | Tarea programada creada |
| 1 / 3 / 11 / 13 | Sysmon | Proceso creado / conexión de red / fichero creado / registro modificado |

---

## Búsquedas realizadas

> Documentar cada búsqueda con su ventana temporal y resultado, para que sea reproducible por otro analista.

| # | Consulta (query literal) | Fuente / índice | Ventana | Resultado |
|---|---|---|---|---|
| 1 | | | | |

```text
usuario:
ip_origen:
host:
event_id:
rule_id:
hash:
dominio:
```

---

## Pivotes recomendados

- Desde la IP origen: ¿qué otros usuarios/hosts ha tocado?
- Desde el usuario: ¿desde qué otras IPs se ha autenticado?
- Desde el host: ¿qué procesos y conexiones tiene en la ventana?
- Desde el hash/dominio: ¿aparece en más activos?

---

## Resultado

- Eventos confirmados:
- Eventos descartados:
- Duplicados:
- Limitaciones (fuentes ausentes, retención insuficiente, campos no recogidos):
