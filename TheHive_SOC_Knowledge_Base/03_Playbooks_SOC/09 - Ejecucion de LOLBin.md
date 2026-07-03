# Ejecución de LOLBin

## Objetivo

Investigar uso de binarios legítimos del sistema (LOLBins) abusados para ejecución, descarga, evasión o persistencia.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0005 Defense Evasion | T1218 System Binary Proxy Execution (.005 mshta, .010 regsvr32, .011 rundll32) |
| TA0011 Command and Control | T1105 Ingress Tool Transfer (certutil, bitsadmin, curl) |
| TA0002 Execution | T1059 Command and Scripting Interpreter |

Referencia de binarios y usos abusivos: proyecto **LOLBAS** (Windows) y **GTFOBins** (Linux).

## Severidad orientativa

- **Medium**: uso anómalo sin confirmación (contexto administrativo posible).
- **High**: LOLBin descargando o ejecutando payload, o lanzado por proceso anómalo.
- **Critical**: confirmación de malware/C2 o uso en cadena de ataque activa.

## Fuentes de datos

- Sysmon EID 1 (CommandLine + padre), 3 (red), 11 (ficheros); Security 4688.
- EDR: árbol de procesos y telemetría de red por proceso.
- Proxy/DNS: destinos contactados por el host en la ventana.

## LOLBins frecuentes y patrón de abuso

| Binario | Abuso típico |
|---|---|
| certutil | Descarga (`-urlcache -f`) y decodificación (`-decode`) |
| bitsadmin | Descarga en segundo plano |
| mshta | Ejecución de HTA/scriptlets remotos |
| rundll32 | Ejecución de DLL maliciosa o javascript |
| regsvr32 | Ejecución remota de scriptlets (squiblydoo) |
| wmic | Ejecución local/remota, reconocimiento |
| msbuild / installutil | Compilar/ejecutar código evadiendo control de aplicaciones |
| curl / wget (Linux y Windows) | Descarga de payloads |
| esentutl / expand / extrac32 | Copia/extracción encubierta |

---

## Binario observado

- Binario y ruta (¿la ruta es la legítima del sistema?):
- Usuario:
- Proceso padre:
- CommandLine completa:
- Hash y firma:
- Timestamp (UTC):

---

## Pasos de investigación

1. Comparar la CommandLine contra el uso documentado en LOLBAS/GTFOBins: ¿coincide con un patrón de abuso conocido?
2. Verificar ruta y firma del binario (un binario renombrado o fuera de `System32` es aún más sospechoso).
3. Analizar el árbol de procesos: quién lo lanzó y qué lanzó él.
4. Correlacionar con red: qué descargó o contactó, y analizar/obtener el payload si es posible.
5. Buscar el fichero descargado/creado y su ejecución posterior.
6. Buscar el mismo patrón en el resto del parque.
7. Contextualizar el host y usuario: ¿equipo de IT/desarrollo (uso legítimo más probable) o usuario ofimático (muy raro)?

---

## Evidencias

| Timestamp (UTC) | Host | Usuario | Binario | CommandLine | Padre | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿La línea de comandos coincide con un patrón de abuso documentado?
- ¿Descarga contenido? ¿De qué dominio/IP y con qué reputación?
- ¿Ejecuta DLL/script/payload? ¿Cuál y dónde quedó?
- ¿El usuario y el proceso padre son esperables para este binario?
- ¿Hay tráfico de red asociado al proceso?
- ¿Hay persistencia o actividad posterior?

## Falsos positivos habituales

- Instaladores y actualizadores legítimos que usan rundll32/regsvr32/msiexec.
- Scripts de IT que usan certutil o bitsadmin (mala práctica, pero legítima): validar y recomendar alternativa.
- Software de gestión y despliegue.

---

## Contención recomendada (si se confirma)

- [ ] Aislar host y matar el proceso
- [ ] Bloquear hash del payload y destinos de red
- [ ] Eliminar el payload y la persistencia
- [ ] Buscar el patrón en todo el parque y contener el resto

## Observables a extraer (TheHive)

hash (payload), url/domain/ip (origen de descarga), filename, other (CommandLine).

---

## Veredicto

- [ ] Uso administrativo legítimo
- [ ] Uso sospechoso sin confirmar
- [ ] Evasión defensiva
- [ ] Malware / loader confirmado
- [ ] Falso positivo
