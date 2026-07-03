# Resumen ejecutivo

> Plantilla principal del caso. Rellenar al abrir el caso y completar antes del cierre.

## Identificación

| Campo | Valor |
|---|---|
| Nombre del caso | |
| ID del caso (TheHive) | |
| Fecha/hora de apertura (UTC) | |
| Fecha/hora de cierre (UTC) | |
| Analista | |
| Equipo / cola | L1 / L2 / L3 / IR |
| Severidad inicial | Low / Medium / High / Critical |
| Severidad final | Low / Medium / High / Critical |
| Estado | Nuevo / En curso / En espera / Cerrado |
| Fuente de detección | SIEM / EDR / NDR / Usuario / Threat Intel / Otro |
| TLP | CLEAR / GREEN / AMBER / AMBER+STRICT / RED |
| PAP | CLEAR / GREEN / AMBER / RED |
| Playbook aplicado | (enlace al playbook de 03_Playbooks_SOC) |
| MITRE ATT&CK | Táctica(s) / Técnica(s), p. ej. TA0006 / T1110 |

---

## Resumen

Describir en 3-5 líneas: qué ocurrió, qué activo o identidad se vio afectada, qué evidencia lo soporta, cuál fue la decisión final y si queda riesgo residual.

> Regla práctica: el resumen debe poder leerse de forma aislada por alguien sin contexto técnico (responsable de turno, CISO) y responder a *qué pasó, a quién afectó y qué se hizo*.

---

## Clasificación

- [ ] Verdadero positivo
- [ ] Verdadero positivo benigno (actividad real pero autorizada)
- [ ] Falso positivo
- [ ] Duplicado
- [ ] Simulación / laboratorio / red team
- [ ] No concluyente (indicar limitación de evidencia)

---

## Vector y causa raíz

- Vector de entrada (phishing, fuerza bruta, vulnerabilidad, credencial filtrada, insider, desconocido):
- Causa raíz (si se conoce):
- ¿Primer caso de este tipo o recurrente?:
- Casos relacionados (IDs):

---

## Impacto

| Área | Impacto (Ninguno / Bajo / Medio / Alto) | Evidencia |
|---|---|---|
| Identidad | | |
| Endpoint | | |
| Red | | |
| Datos | | |
| Servicio | | |
| Negocio | | |

---

## Decisión

- [ ] Cerrar sin acción
- [ ] Cerrar como falso positivo (documentar por qué y si requiere tuning)
- [ ] Escalar a nivel superior (L2 / L3 / IR)
- [ ] Abrir incidente formal
- [ ] Aplicar contención (ver `02_Evidencias_y_Respuesta/05 - Contencion.md`)
- [ ] Requiere mejora de detección (ver `07 - Lecciones aprendidas.md`)
- [ ] Requiere bloqueo de IOC (ver `04 - Observables e IOCs.md`)
- [ ] Requiere comunicación interna / notificación (legal, RRHH, DPO, dirección)

---

## Acciones realizadas

| Acción | Responsable | Fecha/hora (UTC) | Resultado |
|---|---|---|---|
| | | | |

---

## Riesgo residual y seguimiento

- Riesgo residual al cierre:
- Tareas pendientes / seguimiento programado:
- Fecha de revisión:
