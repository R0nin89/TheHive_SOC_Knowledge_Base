# Matriz de severidad SOC

## Severidades

> Equivalencia con TheHive: Low = 1, Medium = 2, High = 3, Critical = 4.

| Severidad | TheHive | Uso | Ejemplos | Tiempo objetivo de triaje | Escalado |
|---|---|---|---|---|---|
| Low | 1 | Evento informativo o de bajo impacto | Cambio esperado, evento aislado, escaneo externo bloqueado | < 24 h | No, salvo recurrencia |
| Medium | 2 | Requiere triaje normal | Cuenta creada sin ticket, escaneo interno leve, phishing reportado sin clic | < 8 h | Solo si cambian criterios |
| High | 3 | Requiere prioridad | Fuerza bruta con login posterior, malware ejecutado, PowerShell ofuscado, reset sospechoso | < 1 h | L2 y aviso al responsable de turno |
| Critical | 4 | Escalado inmediato, posible incidente | C2 confirmado, ransomware, borrado de logs, exfiltración, alta en grupo privilegiado sin ticket | Inmediato (< 15 min) | IR + responsable de turno + dirección de seguridad |

---

## Criterios de subida de severidad

Subir un nivel (acumulables) si:

- Afecta a **cuenta privilegiada** o cuenta de servicio.
- Hay **acceso exitoso** posterior a los intentos.
- Hay **movimiento lateral** confirmado o sospechado.
- Hay **evasión defensiva** (logs borrados, AV/EDR desactivado, exclusiones nuevas).
- Hay **malware ejecutado** (no solo bloqueado).
- Hay indicios de **exfiltración** o acceso a datos sensibles.
- Afecta a **activos críticos** (DC, servidores de negocio, backups, OT).
- **No existe justificación autorizada** (ticket, cambio, mantenimiento).
- Afecta a **múltiples activos o usuarios** (posible campaña).
- El atacante sigue **activo** en el momento del triaje.

---

## Criterios de bajada de severidad

Bajar severidad únicamente si se cumple **al menos uno con evidencia documentada**:

- Existe ticket de cambio aprobado que cubre exactamente la actividad.
- El origen es conocido, autorizado y verificado (no basta con "parece interno").
- El evento es duplicado de un caso ya abierto (enlazar caso).
- La remediación fue automática, completa y validada (p. ej. malware bloqueado en pre-ejecución).
- No hay actividad posterior tras ampliar la ventana de búsqueda.
- Se confirma simulación, laboratorio o ejercicio de red team (con autorización por escrito).

> Nunca bajar severidad solo por ausencia de evidencia si faltan fuentes de log: eso es "no concluyente", no "benigno".

---

## Matriz rápida impacto × confianza

| | Confianza baja (indicios) | Confianza media (evidencia parcial) | Confianza alta (confirmado) |
|---|---|---|---|
| **Impacto bajo** | Low | Low | Medium |
| **Impacto medio** | Medium | Medium | High |
| **Impacto alto** | Medium | High | Critical |
