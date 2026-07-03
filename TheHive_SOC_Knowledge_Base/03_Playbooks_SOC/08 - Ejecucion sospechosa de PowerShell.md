# Ejecución sospechosa de PowerShell

## Objetivo

Investigar ejecuciones de PowerShell con indicadores de descarga, código codificado/ofuscado, evasión o comportamiento anómalo, y determinar qué hizo realmente el script.

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0002 Execution | T1059.001 PowerShell |
| TA0005 Defense Evasion | T1027 Obfuscated Files or Information, T1562.001 Disable or Modify Tools |
| TA0011 Command and Control | T1105 Ingress Tool Transfer |

## Severidad orientativa

- **Medium**: comando sospechoso sin confirmación de malicia (posible administración).
- **High**: comando codificado que descarga/ejecuta contenido remoto, o proceso padre anómalo (Office, navegador).
- **Critical**: confirmación de loader/malware, C2 o robo de credenciales.

## Fuentes de datos

- PowerShell Operational log: EID 4104 (Script Block Logging: el contenido **ya decodificado**), 4103 (module logging).
- Sysmon: EID 1 (proceso + CommandLine + padre), 3 (red), 11 (ficheros).
- Security: 4688 con línea de comandos.
- EDR: árbol de procesos, AMSI.
- Historial: `%APPDATA%\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt`.

---

## Indicadores en línea de comandos

- `-EncodedCommand` / `-enc` / `-e`
- `-ExecutionPolicy Bypass` / `-ep bypass`
- `-WindowStyle Hidden` / `-w hidden`
- `-NoProfile` / `-nop` combinado con lo anterior
- `IEX` / `Invoke-Expression`
- `DownloadString` / `DownloadFile` / `Invoke-WebRequest` / `iwr` / `curl` / `Start-BitsTransfer`
- `FromBase64String`, `[System.Convert]`, compresión (`Gzip`, `Deflate`)
- `Add-MpPreference -ExclusionPath` (exclusiones de Defender)
- PowerShell iniciado por Office (winword, excel), navegador, `wscript/cscript`, `mshta` o tareas desconocidas

---

## Pasos de investigación

1. **Decodificar el comando**: Base64 (UTF-16LE en `-enc`), capas de ofuscación, strings concatenados. El EID 4104 suele darlo ya decodificado.
2. Analizar qué hace el script: ¿descarga (de dónde), ejecuta, persiste, roba credenciales, reconoce el entorno?
3. Analizar el árbol de procesos: padre, abuelo y procesos hijos.
4. Correlacionar con red: conexiones del proceso (Sysmon EID 3 / EDR), dominios e IPs contactados.
5. Buscar ficheros creados o modificados por el proceso.
6. Buscar la **misma línea de comandos o el mismo payload en otros hosts** (¿campaña o caso aislado?).
7. Identificar el origen: adjunto de correo, USB, tarea programada, RMM, administración legítima.

---

## Datos

| Campo | Valor |
|---|---|
| Host | |
| Usuario | |
| Proceso padre (y abuelo) | |
| CommandLine completa | |
| Comando decodificado | |
| Hash del script/payload | |
| Destinos de red contactados | |
| Timestamp (UTC) | |

---

## Evidencias

| Timestamp (UTC) | Host | Usuario | Parent | CommandLine (resumen) | Observación |
|---|---|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿Qué hace el comando una vez decodificado?
- ¿Descarga o ejecuta contenido remoto? ¿El destino es malicioso?
- ¿El proceso padre es coherente (consola admin) o anómalo (Office/navegador)?
- ¿Hay conexiones externas del proceso?
- ¿Hay ficheros creados, tareas o servicios posteriores (persistencia)?
- ¿El usuario es administrador o técnico que usa PowerShell habitualmente?
- ¿Aparece el mismo patrón en más hosts?

## Falsos positivos habituales

- Herramientas de gestión (SCCM, Intune, RMM legítimo, scripts de login) que usan `-enc` y `-nop` de forma rutinaria: identificar por hash/ruta del agente padre y por repetición en todo el parque.
- Instaladores de software (Chocolatey y similares).
- Scripts propios de IT: validar con el equipo, y documentar como exclusión de la regla si procede.

---

## Contención recomendada (si se confirma)

- [ ] Matar el proceso y aislar el host
- [ ] Bloquear hash y dominios/IPs contactados
- [ ] Eliminar persistencia creada
- [ ] Revisar credenciales usadas en el host (posible robo)
- [ ] Buscar y contener el resto de hosts afectados

## Observables a extraer (TheHive)

hash (script/payload), url/domain/ip (descarga y C2), filename, other (CommandLine decodificada como adjunto).

---

## Veredicto

- [ ] Administración legítima
- [ ] Script sospechoso sin confirmar
- [ ] Loader / malware confirmado
- [ ] Evasión defensiva
- [ ] Falso positivo (herramienta de gestión)
