 TheHive SOC Knowledge Base

Base de conocimiento de plantillas y playbooks para gestión de casos SOC en TheHive.

## Estructura

### 01_General_SOC — Plantillas transversales del caso
| Fichero | Uso |
|---|---|
| 01 - Resumen ejecutivo | Ficha principal del caso: identificación, clasificación, impacto, decisión y cierre |
| 02 - Alcance del caso | Qué está afectado y qué se ha descartado |
| 03 - Línea temporal | Timeline en UTC con eventos previos y posteriores |
| 04 - Matriz de severidad | Niveles, SLA de triaje y criterios de subida/bajada |
| 05 - Glosario SOC | Terminología común con referencias MITRE ATT&CK |

### 02_Evidencias_y_Respuesta — Recogida de evidencias y ciclo de respuesta
| Fichero | Uso |
|---|---|
| 01 - Evidencias SIEM | Alertas, campos clave, Event IDs de referencia y búsquedas reproducibles |
| 02 - Evidencias endpoint | Procesos, ficheros, registro y artefactos por SO |
| 03 - Evidencias red | Conexiones, DNS/HTTP/TLS y análisis de beaconing |
| 04 - Observables e IOCs | Observables con dataType, TLP/PAP y decisión de bloqueo |
| 05 - Contención | Acciones, orden recomendado, riesgo residual y validación |
| 06 - Recuperación y cierre | Recuperación, vigilancia post-incidente y criterios de cierre |
| 07 - Lecciones aprendidas | Métricas, mejoras de detección/respuesta/prevención y validación |

### 03_Playbooks_SOC — Playbooks por tipo de alerta
Todos siguen la misma estructura: **Objetivo → MITRE ATT&CK → Severidad orientativa → Fuentes de datos → Datos → Pasos de investigación → Evidencias → Preguntas → Falsos positivos → Contención → Observables → Veredicto**.

| # | Playbook | MITRE principal |
|---|---|---|
| 01 | Fuerza bruta de autenticación | T1110 |
| 02 | Password spraying | T1110.003 |
| 03 | Sospecha de toma de cuenta | T1078, T1098 |
| 04 | Anomalía geográfica de inicio de sesión | T1078 |
| 05 | Acceso remoto sospechoso | T1133, T1021, T1219 |
| 06 | Cambios sensibles de identidad | T1136, T1098 |
| 07 | Cambio en grupo privilegiado | T1078.002, T1098 |
| 08 | Ejecución sospechosa de PowerShell | T1059.001 |
| 09 | Ejecución de LOLBin | T1218, T1105 |
| 10 | Persistencia en endpoint | T1543, T1053, T1547 |
| 11 | Malware detectado | T1204 y según familia |
| 12 | Indicadores de ransomware | T1486, T1490 |
| 13 | Evasión defensiva o borrado de logs | T1070, T1562 |
| 14 | Fuerza bruta SSH Linux | T1110.001, T1098.004 |
| 15 | Abuso de privilegios Linux | T1548.003, T1068 |
| 16 | Escaneo de red o reconocimiento | T1595, T1046 |
| 17 | DNS sospechoso o beaconing C2 | T1071, T1568.002, T1572 |
| 18 | Sospecha de exfiltración de datos | T1048, T1567 |
| 19 | Correo de phishing | T1566 |
| 20 | Explotación de vulnerabilidad | T1190, T1505.003 |

## Cómo usarla

1. Ante una alerta, abrir el caso en TheHive y aplicar el **playbook** correspondiente (03).
2. Documentar evidencias con las plantillas de **02** y clasificar severidad con la matriz de **01/04**.
3. Registrar observables con dataType, TLP y PAP (**02/04**) y decidir bloqueos.
4. Cerrar con **01/01** (resumen), **02/06** (criterios de cierre) y **02/07** (lecciones aprendidas).

## Convenciones

- Timestamps siempre en **UTC**.
- TLP/PAP en todos los casos y observables.
- Todo veredicto debe estar soportado por evidencia documentada; la ausencia de logs se documenta como limitación, no como "benigno".
