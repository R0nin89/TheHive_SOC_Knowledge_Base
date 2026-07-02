# Matriz de severidad SOC

## Severidades

| Severidad | Uso | Ejemplos |
|---|---|---|
| Low | Evento informativo o bajo impacto | cambio esperado, evento aislado |
| Medium | Requiere triaje normal | cuenta creada, escaneo leve, phishing sin clic |
| High | Requiere prioridad | fuerza bruta, malware, reset sospechoso, PowerShell sospechoso |
| Critical | Escalado inmediato | C2, ransomware, log borrado, exfiltración, grupo privilegiado |

---

## Criterios de subida de severidad

Subir severidad si:

- Afecta a cuenta privilegiada.
- Hay acceso exitoso posterior.
- Hay movimiento lateral.
- Hay evasión defensiva.
- Hay malware ejecutado.
- Hay indicios de exfiltración.
- Afecta a activos críticos.
- No existe justificación autorizada.

---

## Criterios de bajada de severidad

Bajar severidad si:

- Hay ticket aprobado.
- El origen es conocido y autorizado.
- El evento es duplicado.
- La remediación fue automática y completa.
- No hay actividad posterior.
- Se confirma simulación o laboratorio.
