# 🐝 TheHive SOC Knowledge Base

> Base de conocimientos SOC en **Markdown** para TheHive, orientada a documentar investigaciones, evidencias, respuesta a incidentes y playbooks de análisis Blue Team.

<p align="center">
  <img src="https://img.shields.io/badge/version-1.0.0-blue" />
  <img src="https://img.shields.io/badge/format-Markdown-green" />
  <img src="https://img.shields.io/badge/platform-TheHive-yellow" />
  <img src="https://img.shields.io/badge/focus-Blue%20Team-informational" />
  <img src="https://img.shields.io/badge/SOC-Knowledge%20Base-purple" />
</p>

---

## 📌 Descripción

**TheHive SOC Knowledge Base** es una colección de notas, plantillas y playbooks en Markdown para crear una base de conocimientos dentro de TheHive.

Está pensada para analistas SOC, laboratorios Blue Team, formación SOC Tier 1 / Tier 2 y documentación interna de investigaciones de seguridad.

El repositorio no contiene información sensible ni datos de una infraestructura concreta. Todo el contenido es **neutro, reutilizable y adaptable**.

---

## 🧠 Objetivo

El objetivo principal es disponer de una estructura clara para documentar:

- Triaje inicial de alertas.
- Evidencias SIEM.
- Evidencias endpoint.
- Evidencias de red.
- Observables e IOCs.
- Contención.
- Recuperación.
- Cierre de casos.
- Lecciones aprendidas.
- Playbooks de investigación SOC.

---

## 📁 Estructura del repositorio

```text
.
├── 01_General_SOC/
│   ├── 01 - Resumen ejecutivo.md
│   ├── 02 - Alcance del caso.md
│   ├── 03 - Linea temporal.md
│   ├── 04 - Matriz de severidad.md
│   └── 05 - Glosario SOC.md
│
├── 02_Evidencias_y_Respuesta/
│   ├── 01 - Evidencias SIEM.md
│   ├── 02 - Evidencias endpoint.md
│   ├── 03 - Evidencias red.md
│   ├── 04 - Observables e IOCs.md
│   ├── 05 - Contencion.md
│   ├── 06 - Recuperacion y cierre.md
│   └── 07 - Lecciones aprendidas.md
│
├── 03_Playbooks_SOC/
│   ├── 01 - Fuerza bruta de autenticacion.md
│   ├── 02 - Password spraying.md
│   ├── 03 - Sospecha de toma de cuenta.md
│   ├── 04 - Anomalia geografica de inicio de sesion.md
│   ├── 05 - Acceso remoto sospechoso.md
│   ├── 06 - Cambios sensibles de identidad.md
│   ├── 07 - Cambio en grupo privilegiado.md
│   ├── 08 - Ejecucion sospechosa de PowerShell.md
│   ├── 09 - Ejecucion de LOLBin.md
│   ├── 10 - Persistencia en endpoint.md
│   ├── 11 - Malware detectado.md
│   ├── 12 - Indicadores de ransomware.md
│   ├── 13 - Evasion defensiva o borrado de logs.md
│   ├── 14 - Fuerza bruta SSH Linux.md
│   ├── 15 - Abuso de privilegios Linux.md
│   ├── 16 - Escaneo de red o reconocimiento.md
│   ├── 17 - DNS sospechoso o beaconing C2.md
│   ├── 18 - Sospecha de exfiltracion de datos.md
│   ├── 19 - Correo de phishing.md
│   └── 20 - Explotacion de vulnerabilidad.md
│
└── README.md
```

---

## 🗂️ Temarios

### 📘 01 - General SOC

Notas base para estructurar cualquier investigación:

| Nota | Uso |
|---|---|
| Resumen ejecutivo | Resumen principal del caso |
| Alcance del caso | Activos, usuarios y servicios afectados |
| Línea temporal | Orden cronológico de eventos |
| Matriz de severidad | Criterios para Low, Medium, High y Critical |
| Glosario SOC | Términos comunes usados en operaciones SOC |

---

### 🧾 02 - Evidencias y respuesta

Notas para documentar evidencias, análisis y acciones tomadas:

| Nota | Uso |
|---|---|
| Evidencias SIEM | Alertas, reglas, eventos y búsquedas |
| Evidencias endpoint | Procesos, ficheros, hashes y actividad local |
| Evidencias red | Conexiones, DNS, IDS, NDR y tráfico sospechoso |
| Observables e IOCs | IPs, dominios, URLs, hashes, usuarios y hosts |
| Contención | Acciones aplicadas para reducir el riesgo |
| Recuperación y cierre | Validación final y cierre del caso |
| Lecciones aprendidas | Mejoras de detección y respuesta |

---

### 🛡️ 03 - Playbooks SOC

Playbooks para investigaciones comunes:

| Playbook | Descripción |
|---|---|
| Fuerza bruta de autenticación | Múltiples intentos fallidos de login |
| Password spraying | Muchos usuarios atacados desde un mismo origen |
| Sospecha de toma de cuenta | Uso anómalo de credenciales válidas |
| Anomalía geográfica de inicio de sesión | Login desde ubicación no habitual |
| Acceso remoto sospechoso | RDP, SSH, VPN u otro acceso remoto anómalo |
| Cambios sensibles de identidad | Cambios en cuentas, contraseñas o grupos |
| Cambio en grupo privilegiado | Alta o baja en grupos críticos |
| Ejecución sospechosa de PowerShell | PowerShell con descarga, bypass o codificación |
| Ejecución de LOLBin | Uso sospechoso de binarios legítimos |
| Persistencia en endpoint | Servicios, tareas, registro, cron o systemd |
| Malware detectado | Detección y validación de malware |
| Indicadores de ransomware | Cifrado masivo o nota de rescate |
| Evasión defensiva o borrado de logs | Logs borrados o controles modificados |
| Fuerza bruta SSH Linux | Intentos fallidos SSH repetidos |
| Abuso de privilegios Linux | Uso anómalo de sudo, su o root |
| Escaneo de red o reconocimiento | Escaneo de puertos o enumeración |
| DNS sospechoso o beaconing C2 | DNS raro, túnel DNS o conexiones periódicas |
| Sospecha de exfiltración de datos | Transferencia anómala de información |
| Correo de phishing | Email sospechoso, URL o adjunto malicioso |
| Explotación de vulnerabilidad | Intento o explotación de CVE o servicio vulnerable |
---

## 🚀 Instalación / uso

### Opción 1: clonar el repositorio

```bash
git clone https://github.com/TU_USUARIO/TheHive_SOC_Knowledge_Base.git
cd TheHive_SOC_Knowledge_Base
```

### Opción 2: descargar como ZIP

1. Pulsar **Code**.
2. Pulsar **Download ZIP**.
3. Extraer el contenido.
4. Copiar las notas necesarias.

---

## 🐝 Uso en TheHive

TheHive utiliza la base de conocimientos como una Wiki. Por eso el uso recomendado es manual:

1. Entrar en **TheHive**.
2. Ir a **Base de conocimientos**.
3. Pulsar `+`.
4. Crear una página nueva.
5. Copiar el contenido de una nota `.md`.
6. Pegar el contenido.
7. Guardar.
8. Repetir con las páginas necesarias.

Ejemplo:

```text
Fichero:
03_Playbooks_SOC/01 - Fuerza bruta de autenticacion.md

Página en TheHive:
Fuerza bruta de autenticación
```

---

## 🔎 Flujo recomendado de investigación

```text
Alerta inicial
      ↓
Resumen ejecutivo
      ↓
Alcance del caso
      ↓
Línea temporal
      ↓
Evidencias SIEM / endpoint / red
      ↓
Observables e IOCs
      ↓
Playbook específico
      ↓
Contención
      ↓
Recuperación y cierre
      ↓
Lecciones aprendidas
```

---

## 🧩 Clasificación de casos

| Clasificación | Descripción |
|---|---|
| Verdadero positivo | Actividad maliciosa o no autorizada confirmada |
| Falso positivo | La alerta no representa actividad maliciosa |
| Actividad autorizada | El evento corresponde a una acción aprobada |
| Duplicado | Ya existe otro caso o alerta equivalente |
| Simulación / laboratorio | Actividad generada como prueba controlada |
| No concluyente | No hay evidencia suficiente para confirmar o descartar |

---

## 🚦 Severidad recomendada

| Severidad | Cuándo usarla |
|---|---|
| Low | Evento informativo o de bajo impacto |
| Medium | Requiere análisis normal |
| High | Requiere análisis prioritario |
| Critical | Requiere escalado inmediato |

Subir la severidad cuando exista:

- Cuenta privilegiada afectada.
- Login exitoso tras múltiples fallos.
- Malware ejecutado.
- Movimiento lateral.
- Exfiltración.
- Borrado de logs.
- Desactivación de controles.
- Persistencia confirmada.
- Afectación a sistemas críticos.

---

## ✅ Buenas prácticas

- No incluir contraseñas.
- No incluir API keys.
- No pegar datos personales innecesarios.
- Separar hechos, hipótesis y conclusiones.
- Documentar siempre la fuente de cada evidencia.
- Mantener una línea temporal clara.
- Registrar acciones de contención y su resultado.
- Añadir lecciones aprendidas al cierre.
- Revisar periódicamente los playbooks.

---

## 🧪 Casos de uso

Este repositorio puede usarse para:

- Crear una base de conocimientos en TheHive.
- Documentar procedimientos SOC.
- Estandarizar investigaciones.
- Preparar laboratorios Blue Team.
- Formar analistas SOC Tier 1 / Tier 2.
- Crear playbooks internos.
- Documentar simulaciones de seguridad.
- Mejorar la trazabilidad de casos.

---

## ❌ Lo que no incluye

Este repositorio no incluye:

- Reglas SIEM.
- Reglas Sigma.
- Reglas YARA.
- Reglas Suricata.
- Automatizaciones SOAR.
- Credenciales.
- Datos reales de incidentes.
- Información de infraestructura interna.

---

## 🛠️ Posibles mejoras futuras

- Añadir capturas de TheHive.
- Añadir plantillas de casos.
- Añadir ejemplos de casos cerrados.
- Añadir reglas Sigma relacionadas.
- Añadir mapeo MITRE ATT&CK por playbook.
- Añadir checklist SOC Tier 1.
- Añadir procedimientos de escalado SOC Tier 2.
- Añadir versión en inglés.

---

## 📄 Licencia

Uso libre para laboratorios, formación y documentación interna SOC.

Puedes adaptar, modificar y ampliar las notas según las necesidades de tu entorno.

---

## 👤 Autor

Proyecto de documentación SOC para uso en laboratorios Blue Team y gestión de casos con TheHive.


