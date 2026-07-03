# TheHive SOC Knowledge Base

Base de conocimiento para la gestión de casos SOC en **TheHive**.

Este repositorio contiene plantillas, playbooks y guías operativas para documentar, investigar, clasificar, responder y cerrar casos de seguridad de forma homogénea.

---

## Objetivo

Estandarizar el trabajo del analista SOC durante el ciclo completo de un caso:

1. Recepción y clasificación de la alerta.
2. Triaje inicial.
3. Recogida de evidencias.
4. Investigación técnica.
5. Decisión de severidad.
6. Contención y recuperación.
7. Cierre documentado.
8. Lecciones aprendidas.

---

## Estructura del repositorio

```text
TheHive-SOC-Knowledge-Base/
├── 01_General_SOC/
│   ├── 01 - Resumen ejecutivo.md
│   ├── 02 - Alcance del caso.md
│   ├── 03 - Línea temporal.md
│   ├── 04 - Matriz de severidad.md
│   └── 05 - Glosario SOC.md
│
├── 02_Evidencias_y_Respuesta/
│   ├── 01 - Evidencias SIEM.md
│   ├── 02 - Evidencias endpoint.md
│   ├── 03 - Evidencias red.md
│   ├── 04 - Observables e IOCs.md
│   ├── 05 - Contención.md
│   ├── 06 - Recuperación y cierre.md
│   └── 07 - Lecciones aprendidas.md
│
└── 03_Playbooks_SOC/
    ├── 01 - Fuerza bruta de autenticación.md
    ├── 02 - Password spraying.md
    ├── 03 - Sospecha de toma de cuenta.md
    ├── 04 - Anomalía geográfica de inicio de sesión.md
    ├── 05 - Acceso remoto sospechoso.md
    ├── 06 - Cambios sensibles de identidad.md
    ├── 07 - Cambio en grupo privilegiado.md
    ├── 08 - Ejecución sospechosa de PowerShell.md
    ├── 09 - Ejecución de LOLBin.md
    ├── 10 - Persistencia en endpoint.md
    ├── 11 - Malware detectado.md
    ├── 12 - Indicadores de ransomware.md
    ├── 13 - Evasión defensiva o borrado de logs.md
    ├── 14 - Fuerza bruta SSH Linux.md
    ├── 15 - Abuso de privilegios Linux.md
    ├── 16 - Escaneo de red o reconocimiento.md
    ├── 17 - DNS sospechoso o beaconing C2.md
    ├── 18 - Sospecha de exfiltración de datos.md
    ├── 19 - Correo de phishing.md
    └── 20 - Explotación de vulnerabilidad.md
```

---

## 01_General_SOC

Plantillas transversales para documentar información general del caso.

| Fichero | Uso |
|---|---|
| `01 - Resumen ejecutivo.md` | Ficha principal del caso: identificación, clasificación, impacto, decisión y cierre. |
| `02 - Alcance del caso.md` | Define qué está afectado, qué sistemas se han revisado y qué queda descartado. |
| `03 - Línea temporal.md` | Timeline en UTC con eventos previos, durante y posteriores al incidente. |
| `04 - Matriz de severidad.md` | Niveles de severidad, SLA de triaje y criterios de subida/bajada. |
| `05 - Glosario SOC.md` | Terminología común SOC con referencias a MITRE ATT&CK. |

---

## 02_Evidencias_y_Respuesta

Plantillas para registrar evidencias técnicas, acciones de respuesta y cierre operativo.

| Fichero | Uso |
|---|---|
| `01 - Evidencias SIEM.md` | Alertas, campos clave, Event IDs de referencia y búsquedas reproducibles. |
| `02 - Evidencias endpoint.md` | Procesos, ficheros, registro, servicios, tareas programadas y artefactos por sistema operativo. |
| `03 - Evidencias red.md` | Conexiones, DNS, HTTP, TLS, proxy, firewall, NDR y análisis de beaconing. |
| `04 - Observables e IOCs.md` | Registro de observables con `dataType`, `TLP`, `PAP`, fuente, confianza y decisión de bloqueo. |
| `05 - Contención.md` | Acciones de contención, orden recomendado, riesgo residual y validación posterior. |
| `06 - Recuperación y cierre.md` | Recuperación, vigilancia post-incidente, criterios de cierre y validación final. |
| `07 - Lecciones aprendidas.md` | Métricas, mejoras de detección, respuesta, prevención y validación de controles. |

---

## 03_Playbooks_SOC

Playbooks de investigación por tipo de alerta.

Todos los playbooks siguen la misma estructura:

```text
Objetivo
MITRE ATT&CK
Severidad orientativa
Fuentes de datos
Datos necesarios
Pasos de investigación
Evidencias esperadas
Preguntas de triaje
Falsos positivos comunes
Contención
Observables e IOCs
Veredicto
```

| Nº | Playbook | MITRE ATT&CK principal |
|---:|---|---|
| 01 | Fuerza bruta de autenticación | `T1110` |
| 02 | Password spraying | `T1110.003` |
| 03 | Sospecha de toma de cuenta | `T1078`, `T1098` |
| 04 | Anomalía geográfica de inicio de sesión | `T1078` |
| 05 | Acceso remoto sospechoso | `T1133`, `T1021`, `T1219` |
| 06 | Cambios sensibles de identidad | `T1136`, `T1098` |
| 07 | Cambio en grupo privilegiado | `T1078.002`, `T1098` |
| 08 | Ejecución sospechosa de PowerShell | `T1059.001` |
| 09 | Ejecución de LOLBin | `T1218`, `T1105` |
| 10 | Persistencia en endpoint | `T1543`, `T1053`, `T1547` |
| 11 | Malware detectado | `T1204` y técnica según familia |
| 12 | Indicadores de ransomware | `T1486`, `T1490` |
| 13 | Evasión defensiva o borrado de logs | `T1070`, `T1562` |
| 14 | Fuerza bruta SSH Linux | `T1110.001`, `T1098.004` |
| 15 | Abuso de privilegios Linux | `T1548.003`, `T1068` |
| 16 | Escaneo de red o reconocimiento | `T1595`, `T1046` |
| 17 | DNS sospechoso o beaconing C2 | `T1071`, `T1568.002`, `T1572` |
| 18 | Sospecha de exfiltración de datos | `T1048`, `T1567` |
| 19 | Correo de phishing | `T1566` |
| 20 | Explotación de vulnerabilidad | `T1190`, `T1505.003` |

---

## Flujo recomendado de uso

Ante una alerta en TheHive:

1. Crear o abrir el caso correspondiente.
2. Aplicar el playbook adecuado desde `03_Playbooks_SOC`.
3. Documentar el resumen del caso con `01_General_SOC/01 - Resumen ejecutivo.md`.
4. Definir el alcance con `01_General_SOC/02 - Alcance del caso.md`.
5. Construir la línea temporal con `01_General_SOC/03 - Línea temporal.md`.
6. Registrar evidencias usando las plantillas de `02_Evidencias_y_Respuesta`.
7. Clasificar la severidad con `01_General_SOC/04 - Matriz de severidad.md`.
8. Registrar observables e IOCs con `02_Evidencias_y_Respuesta/04 - Observables e IOCs.md`.
9. Ejecutar acciones de contención si procede.
10. Validar recuperación y cierre.
11. Documentar lecciones aprendidas.

---

## Convenciones de documentación

| Elemento | Convención |
|---|---|
| Timestamps | Siempre en UTC. |
| Severidad | Usar equivalencia TheHive: `Low = 1`, `Medium = 2`, `High = 3`, `Critical = 4`. |
| TLP | Todo caso y observable debe tener clasificación TLP. |
| PAP | Todo observable accionable debe tener clasificación PAP. |
| Evidencia | Todo veredicto debe estar soportado por evidencia documentada. |
| Ausencia de logs | Documentar como limitación de visibilidad, no como benigno. |
| MITRE ATT&CK | Asociar técnicas cuando exista relación clara con la actividad observada. |
| Observables | Registrar tipo, valor, fuente, confianza, TLP, PAP y decisión operativa. |

---

## Criterios generales de severidad

| Severidad | TheHive | Uso orientativo |
|---|---:|---|
| 🟢 **Low** | 1 | Evento informativo, bajo impacto o actividad contenida. |
| 🟡 **Medium** | 2 | Requiere triaje, pero sin compromiso confirmado. |
| 🔴 **High** | 3 | Evidencia fuerte de actividad maliciosa, ejecución o impacto relevante. |
| 🟣 **Critical** | 4 | Compromiso confirmado, impacto alto, exfiltración, ransomware o atacante activo. |

---

## Buenas prácticas SOC

- No cerrar un caso como benigno sin evidencia suficiente.
- No bajar severidad solo porque no se ha encontrado más actividad.
- Ampliar la ventana temporal antes de cerrar.
- Validar si existe ticket, cambio aprobado o mantenimiento.
- Revisar actividad posterior al evento inicial.
- Documentar fuentes revisadas y fuentes no disponibles.
- Registrar observables aunque no se bloqueen.
- Distinguir entre `no observado`, `descartado` y `no concluyente`.
- Enlazar casos duplicados o relacionados.
- Mantener consistencia en nombres de usuarios, hosts, IPs y dominios.

---

## Estados recomendados de veredicto

| Veredicto | Uso |
|---|---|
| **True Positive** | Actividad maliciosa o no autorizada confirmada. |
| **False Positive** | Actividad legítima confirmada con evidencia suficiente. |
| **Benign True Positive** | Actividad real detectada, pero autorizada o esperada. |
| **No concluyente** | No hay evidencia suficiente o existen limitaciones de visibilidad. |
| **Duplicado** | Caso ya investigado o integrado en otro caso. |

---

## Cierre de casos

Un caso puede cerrarse únicamente cuando:

- La severidad ha sido justificada.
- El alcance ha sido definido.
- Las evidencias principales han sido documentadas.
- Los observables relevantes han sido registrados.
- Se ha revisado actividad posterior.
- Se han documentado las limitaciones de visibilidad.
- Se han ejecutado o descartado acciones de contención.
- Existe un veredicto final soportado por evidencia.

---

## Nota operativa

La ausencia de evidencia no debe interpretarse automáticamente como ausencia de compromiso.

Cuando falten fuentes de log, visibilidad EDR, telemetría de red o contexto de negocio, el resultado debe documentarse como:

> No se identifican evidencias adicionales con las fuentes disponibles. El resultado queda como **no concluyente** debido a limitaciones de visibilidad.
