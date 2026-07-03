# Lecciones aprendidas y mejora de detección

> Rellenar en las 48-72 h posteriores al cierre, con el caso fresco. En incidentes High/Critical, hacerlo en sesión conjunta (analistas implicados + responsable), sin buscar culpables: el objetivo es el proceso, no las personas.

## Métricas del caso

- Tiempo hasta detección (desde primer evento malicioso):
- Tiempo hasta triaje (desde la alerta):
- Tiempo hasta contención:
- Tiempo hasta cierre:
- ¿Se cumplieron los SLA de la matriz de severidad?:

---

## Qué funcionó

-
-
-

## Qué faltó o falló

> Considerar: visibilidad (¿faltaban logs?), detección (¿la regla llegó tarde o no existía?), proceso (¿el playbook cubría el caso?), herramientas, comunicación y conocimiento.

-
-
-

---

## Mejora de detección

| Mejora | Tipo (nueva regla / umbral / FP / caso de uso / nueva fuente de log) | Prioridad | Fuente de datos | MITRE ATT&CK cubierto | Responsable | Estado |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Mejora de respuesta

| Mejora (playbook, automatización, permisos, contactos) | Prioridad | Responsable | Estado |
|---|---|---|---|
| | | | |

---

## Mejora de prevención

| Mejora (parcheo, hardening, MFA, segmentación, concienciación) | Prioridad | Responsable | Estado |
|---|---|---|---|
| | | | |

---

## Validación: pruebas recomendadas

> Toda regla nueva o ajustada debe probarse. Ejecutar solo en entorno autorizado y coordinado con el SOC (purple team / simulación controlada).

- [ ] Simular fuerza bruta
- [ ] Simular password spraying
- [ ] Simular ejecución PowerShell ofuscado
- [ ] Simular uso de LOLBins
- [ ] Simular persistencia (servicio, tarea programada, cron)
- [ ] Simular borrado de logs
- [ ] Simular C2 / beaconing
- [ ] Simular exfiltración (volumen controlado)
- [ ] Verificar que la alerta llega, con la severidad y los campos esperados

---

## Actualización de esta KB

- ¿Este caso requiere actualizar algún playbook o plantilla? ¿Cuál y por qué?:
