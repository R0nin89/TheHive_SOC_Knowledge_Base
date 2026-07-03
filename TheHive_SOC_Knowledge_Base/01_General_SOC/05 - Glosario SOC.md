# Glosario SOC

## Conceptos generales

| Término | Significado |
|---|---|
| IOC | Indicador de compromiso: IP, dominio, URL, hash, email, usuario o host asociado a actividad maliciosa |
| IOA | Indicador de ataque: patrón de comportamiento (no artefacto estático) que sugiere actividad ofensiva en curso |
| TTP | Táctica, técnica y procedimiento usado por un atacante (marco de referencia: MITRE ATT&CK) |
| MITRE ATT&CK | Base de conocimiento de tácticas (TA) y técnicas (T) de atacantes; se usa para clasificar casos y detecciones |
| SIEM | Plataforma de correlación y análisis de eventos de seguridad |
| EDR | Telemetría, detección y respuesta en endpoint |
| XDR | Detección y respuesta extendida: correlaciona endpoint, red, identidad y correo |
| NDR | Telemetría y detección en red |
| IDS / IPS | Sistema de detección / prevención de intrusiones |
| SOAR | Orquestación y automatización de respuesta (p. ej. TheHive + Cortex) |
| TheHive | Plataforma de gestión de casos e incidentes de seguridad |
| Cortex | Motor de análisis y respuesta de TheHive (analyzers y responders sobre observables) |
| MISP | Plataforma de compartición de inteligencia de amenazas |
| TLP | Traffic Light Protocol: nivel de compartición de la información (CLEAR, GREEN, AMBER, AMBER+STRICT, RED) |
| PAP | Permissible Actions Protocol: qué acciones se pueden realizar con un observable sin alertar al atacante |
| SLA | Acuerdo de nivel de servicio: tiempos objetivo de triaje, respuesta y resolución |
| Dwell time | Tiempo entre el compromiso inicial y su detección |

## Clasificación de alertas

| Término | Significado |
|---|---|
| Verdadero positivo | Actividad maliciosa o no autorizada confirmada |
| Verdadero positivo benigno | La detección funcionó, pero la actividad era legítima/autorizada (p. ej. pentest) |
| Falso positivo | La alerta no corresponde a actividad maliciosa; suele requerir tuning |
| Falso negativo | Actividad maliciosa que no generó alerta; alimenta la mejora de detección |
| Triaje | Evaluación inicial de una alerta para decidir prioridad, veredicto y escalado |

## Técnicas y actividad del atacante

| Término | Significado |
|---|---|
| Toma de cuenta (ATO) | Uso no autorizado de credenciales válidas |
| Brute force | Muchos intentos de contraseña contra una o varias cuentas (T1110) |
| Password spraying | Pocas contraseñas probadas contra muchos usuarios para evitar bloqueos (T1110.003) |
| Credential stuffing | Uso de credenciales filtradas de otros servicios (T1110.004) |
| MFA fatigue / push bombing | Envío masivo de notificaciones MFA hasta que la víctima acepta |
| Phishing | Correo fraudulento para robar credenciales o entregar malware (T1566) |
| BEC | Business Email Compromise: fraude mediante suplantación o compromiso de correo corporativo |
| LOLBin | Binario legítimo del sistema usado con fines maliciosos (certutil, mshta, rundll32...) |
| Living off the land | Operar usando solo herramientas nativas del sistema para evitar detección |
| Movimiento lateral | Desplazamiento del atacante entre sistemas internos (TA0008) |
| Escalada de privilegios | Obtención de permisos superiores a los iniciales (TA0004) |
| Persistencia | Mecanismo para mantener acceso tras reinicios o cambios de credenciales (TA0003) |
| Evasión defensiva | Acción para ocultar actividad o desactivar controles (TA0005) |
| C2 | Canal de mando y control entre el malware y la infraestructura del atacante (TA0011) |
| Beaconing | Comunicación periódica y regular hacia infraestructura externa, típica de C2 |
| DGA | Algoritmo de generación de dominios usado por malware para localizar su C2 |
| Túnel DNS | Exfiltración o C2 encapsulado en consultas DNS |
| Exfiltración | Salida no autorizada de datos (TA0010) |
| Ransomware | Malware que cifra datos y exige rescate; suele incluir exfiltración previa (doble extorsión) |
| Webshell | Script malicioso en un servidor web que da acceso remoto al atacante |
| Dropper / loader | Malware cuya función es descargar o ejecutar otro malware |
| PUA / PUP | Aplicación potencialmente no deseada; molesta o arriesgada, no necesariamente maliciosa |
