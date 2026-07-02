# Ejecución sospechosa de PowerShell

## Objetivo

Investigar PowerShell con indicadores de descarga, ejecución codificada, evasión o comportamiento anómalo.

---

## Indicadores

- `-EncodedCommand`
- `-enc`
- `Bypass`
- `Hidden`
- `IEX`
- `DownloadString`
- `Invoke-WebRequest`
- `Start-BitsTransfer`
- PowerShell iniciado por Office, navegador o script no esperado

---

## Datos

| Campo | Valor |
|---|---|
| Host | |
| Usuario | |
| Proceso padre | |
| CommandLine | |
| Hash | |
| Destino red | |
| Timestamp | |

---

## Evidencias

| Timestamp | Host | Usuario | Parent | CommandLine | Observación |
|---|---|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿Se puede decodificar el comando?
- ¿Descarga o ejecuta contenido remoto?
- ¿El proceso padre es sospechoso?
- ¿Hay conexiones externas?
- ¿Hay ficheros creados?
- ¿Hay persistencia posterior?

---

## Veredicto

- [ ] Administración legítima
- [ ] Script sospechoso
- [ ] Loader / malware
- [ ] Falso positivo
