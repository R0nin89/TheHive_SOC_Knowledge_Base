# Sospecha de exfiltración de datos

## Objetivo

Investigar transferencias anómalas de datos hacia destinos no habituales y determinar qué datos salieron, cuántos, hacia dónde y por quién.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0010 Exfiltration | T1048 Exfiltration Over Alternative Protocol, T1567.002 Exfiltration to Cloud Storage |
| TA0009 Collection | T1560 Archive Collected Data, T1005 Data from Local System |

## Severidad orientativa

- **Medium**: volumen anómalo sin confirmar contenido ni malicia.
- **High**: transferencia confirmada a destino no corporativo de datos internos, o exfiltración por insider.
- **Critical**: datos sensibles/personales confirmados, exfiltración por atacante, o volumen masivo (valorar obligaciones legales de notificación).

## Fuentes de datos

- Proxy / firewall / NetFlow: bytes salientes por host y destino, categoría del destino.
- DLP y logs de aplicaciones cloud (compartición externa, descargas masivas).
- EDR: proceso que genera el tráfico, uso de herramientas de sincronización/transferencia (rclone, MEGAsync, FileZilla, WinSCP, curl).
- Auditoría de ficheros (4663) y de plataformas documentales: qué se leyó antes de salir.
- Correo: adjuntos salientes voluminosos, reenvíos.

---

## Datos

| Campo | Valor |
|---|---|
| Host / usuario origen | |
| Destino (dominio/IP, servicio, ¿personal o corporativo?) | |
| Volumen (y ratio out/in) | |
| Protocolo / método (HTTPS, DNS, correo, USB, cloud) | |
| Herramienta o proceso | |
| Duración / ¿sigue activo? | |
| Timestamp (UTC) | |

---

## Pasos de investigación

1. Establecer línea base del host/usuario: ¿ese volumen y destino son nuevos o habituales (backups, sincronización corporativa)?
2. Identificar el proceso responsable del tráfico (EDR) y la herramienta (rclone y similares son bandera roja).
3. Reconstruir la fase de **recolección previa**: accesos masivos a ficheros/repositorios, creación de archivos comprimidos grandes (zip/rar/7z, a menudo con contraseña), staging en carpetas temporales.
4. Determinar el contenido si es posible (nombres de fichero en logs DLP/auditoría, tamaño del archivo comprimido vs datos accedidos).
5. Clasificar al actor: atacante externo (buscar compromiso previo: C2, cuenta tomada) vs insider (contexto: salida de la empresa, accesos fuera de su rol).
6. Cuantificar: ventana completa de la exfiltración (¿días/semanas?), bytes totales, nº de ficheros.
7. Si hay datos personales o regulados: escalar a DPO/legal (posible notificación en plazo).

---

## Evidencias

| Timestamp (UTC) | Origen | Destino | Protocolo | Volumen | Proceso/herramienta | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿El volumen y destino son anómalos frente a la línea base?
- ¿Qué proceso/herramienta genera la transferencia?
- ¿Hubo compresión/cifrado y staging previo?
- ¿Qué datos se accedieron antes (y su clasificación)?
- ¿Hay compromiso previo del host/cuenta (atacante) o es un insider?
- ¿La transferencia sigue activa ahora?
- ¿Aplican obligaciones de notificación (RGPD u otras)?

## Falsos positivos habituales

- Backups y sincronizaciones corporativas (OneDrive/Drive/Dropbox de empresa) — la causa más común de picos.
- Subidas legítimas a proveedores/clientes (proyectos, entregas).
- Actualizaciones P2P, telemetría, réplicas entre CPDs.
- Uso personal tolerado de nube (violación de política, no incidente, según normas internas).

---

## Contención recomendada (si se confirma)

- [ ] Cortar la transferencia (bloquear destino, aislar host)
- [ ] Deshabilitar cuenta / revocar sesiones si hay compromiso o insider activo
- [ ] Preservar evidencias (logs, archivo staging, memoria) — clave si habrá acciones legales/laborales
- [ ] Solicitar eliminación al servicio destino si es viable (legal)
- [ ] Escalar a DPO/legal/RRHH según actor y datos

## Observables a extraer (TheHive)

domain/ip/url (destino), hash y filename (archivos staging, herramienta), other (cuenta, volumen).

---

## Veredicto

- [ ] Transferencia legítima (backup/sincronización/negocio)
- [ ] Exfiltración sospechosa sin confirmar
- [ ] Exfiltración confirmada por atacante (→ incidente)
- [ ] Exfiltración por insider (→ RRHH/legal)
- [ ] Violación de política sin malicia
- [ ] Falso positivo
