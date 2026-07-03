# Indicadores de ransomware

## Objetivo

Investigar actividad compatible con cifrado masivo, destrucción de datos o nota de rescate. **Este playbook prioriza velocidad: contener primero, investigar en paralelo.**

## MITRE ATT&CK

| Táctica | Técnica |
|---|---|
| TA0040 Impact | T1486 Data Encrypted for Impact, T1490 Inhibit System Recovery |
| TA0010 Exfiltration | T1567 Exfiltration Over Web Service (doble extorsión) |
| TA0005 Defense Evasion | T1562.001 Disable Security Tools, T1070.001 Clear Windows Event Logs |

## Severidad orientativa

**Critical por defecto.** Activar el proceso de escalado inmediato (IR + responsable de turno) ante indicios razonables, sin esperar confirmación completa.

## Fuentes de datos

- EDR: procesos con I/O masivo de ficheros, detecciones de ransomware.
- File servers: auditoría de ficheros (4663), renombrados masivos, honeyfiles.
- Indicadores previos: `vssadmin delete shadows`, `wmic shadowcopy delete`, `bcdedit /set recoveryenabled no`, `wbadmin delete catalog` — suelen preceder al cifrado.
- Backups: logs de acceso/borrado de copias.

---

## Acciones inmediatas (primeros minutos, en paralelo a la investigación)

1. **Aislar** los hosts afectados (network containment). No apagarlos si es viable aislar: se pierde memoria volátil.
2. Identificar la **cuenta que cifra** (propietario de los ficheros modificados en shares) y **deshabilitarla + revocar sesiones**.
3. **Proteger los backups**: desconectar/aislar el sistema de backup y verificar su integridad antes de nada.
4. Cortar acceso a los shares afectados si el cifrado continúa.
5. Escalar a IR y responsable de turno. Preservar evidencias (nota de rescate, muestra cifrada, muestra del binario).

---

## Indicadores

- Modificación/renombrado masivo de ficheros (ritmo, extensión nueva):
- Nota de rescate (nombre de fichero, contenido, familia si es identificable):
- Proceso responsable y hash:
- Cuenta usada para cifrar:
- Origen del cifrado (¿un host cifra los shares o cada host se cifra localmente?):
- Shadow copies / backups borrados:
- ¿Hay indicios de exfiltración previa? (doble extorsión: revisar días/semanas antes):
- Timestamp de inicio (UTC):

---

## Investigación (en paralelo)

1. Identificar familia por la nota/extensión (condiciona TTPs conocidos y posibilidad de descifrado público).
2. Reconstruir la cadena: acceso inicial (RDP/VPN/phishing/vulnerabilidad) → escalada → lateralidad → despliegue. El cifrado es el **final** del ataque; el compromiso puede llevar días o semanas.
3. Delimitar alcance: hosts cifrados, hosts comprometidos pero no cifrados (¡también están comprometidos!), cuentas usadas.
4. Buscar exfiltración previa (picos de tráfico saliente, herramientas tipo rclone/MEGA/FileZilla).
5. Verificar estado real de los backups: existencia, integridad, aislamiento, fecha del último punto sano.

---

## Evidencias

| Timestamp (UTC) | Host | Ruta | Acción | Proceso | Cuenta | Observación |
|---|---|---|---|---|---|---|
| | | | | | | |

---

## Preguntas

- ¿El cifrado está activo ahora mismo?
- ¿Qué cuenta y qué host origen están cifrando los shares?
- ¿Los backups están intactos y aislados?
- ¿Hay nota de rescate y de qué familia?
- ¿Hubo exfiltración previa (doble extorsión)?
- ¿Cuál fue el acceso inicial y sigue abierto?
- ¿Hay que activar el plan de crisis / notificaciones (dirección, legal, DPO, ciberseguro, autoridad)?

## Falsos positivos habituales

- Cifrado corporativo legítimo (BitLocker, DLP, herramientas de cifrado de ficheros) desplegándose.
- Migraciones o renombrados masivos por scripts de IT.
- Actualizaciones que tocan muchos ficheros.

> Diferenciador rápido: el ransomware suele cambiar extensiones a una desconocida uniforme, dejar notas TXT/HTA en cada carpeta y borrar shadow copies.

---

## Observables a extraer (TheHive)

hash (binario), filename (nota, extensión), ip/domain (C2, exfiltración), other (cuenta usada, dirección de la nota).

---

## Veredicto / estado

- [ ] Ransomware activo contenido
- [ ] Ransomware consumado (cifrado completado)
- [ ] Intento bloqueado por EDR
- [ ] Actividad legítima (cifrado/migración corporativa)
- [ ] Falso positivo
