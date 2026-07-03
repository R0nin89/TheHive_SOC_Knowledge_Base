# Observables e IOCs

> En TheHive, cada observable debe llevar: **dataType**, valor, TLP, PAP, flag IOC (sí/no), flag "sighted" y tags. Marcar como IOC solo lo que tenga valor de detección/bloqueo.

## Observables

| dataType (TheHive) | Valor | Fuente | TLP | PAP | ¿IOC? | ¿Avistado (sighted)? | Reputación | Acción |
|---|---|---|---|---|---|---|---|---|
| ip | | | | | | | | |
| domain | | | | | | | | |
| url | | | | | | | | |
| hash | | | | | | | | |
| mail | | | | | | | | |
| mail-subject | | | | | | | | |
| filename | | | | | | | | |
| user-agent | | | | | | | | |
| registry | | | | | | | | |
| hostname | | | | | | | | |
| other (usuario, ASN...) | | | | | | | | |

---

## Enriquecimiento

> Con Cortex: lanzar analyzers sobre cada observable y documentar el resultado. Respetar el PAP: con PAP:RED no realizar consultas activas que puedan alertar al atacante (p. ej. resolver el dominio, visitar la URL).

| Observable | Analyzer / fuente de enriquecimiento | Resultado | Confianza (Alta/Media/Baja) | Fecha de consulta |
|---|---|---|---|---|
| | | | | |

---

## Contexto que resta valor al IOC (evitar bloqueos con daño colateral)

- ¿La IP es de un proveedor cloud / CDN / VPN compartida? (bloquearla puede afectar servicios legítimos)
- ¿El dominio es un servicio legítimo abusado (Drive, Dropbox, GitHub, Telegram)?
- ¿El hash corresponde a una herramienta de doble uso (PsExec, AnyDesk, nmap)?

---

## Decisión sobre IOCs

- [ ] Bloquear IP (firewall / proxy) — vigencia del bloqueo:
- [ ] Bloquear dominio / URL (DNS / proxy / correo)
- [ ] Bloquear hash (EDR / AV)
- [ ] Monitorizar (crear regla de detección sin bloquear)
- [ ] Añadir a inteligencia de amenazas (MISP) y compartir según TLP
- [ ] Solo documentar (sin valor de detección)

---

## Revisión de vigencia

- Fecha de revisión de los bloqueos (los IOCs caducan; las IPs se reciclan):
- Responsable de la revisión:
