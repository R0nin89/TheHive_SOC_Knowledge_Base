# Alcance del caso

> Objetivo: delimitar qué está afectado y, tan importante como eso, qué se ha revisado y descartado. Un alcance sin "descartados" está incompleto.

## Activos afectados

| Activo (hostname/FQDN) | Tipo | Criticidad (Alta/Media/Baja) | Rol / función | SO / versión | Estado (Afectado / Sospechoso / Limpio / Contenido) |
|---|---|---|---|---|---|
| | Endpoint | | | | |
| | Servidor | | | | |
| | Cuenta | | | | |
| | Servicio / SaaS | | | | |

---

## Usuarios / identidades afectadas

| Usuario | Tipo de cuenta | Privilegios | MFA | Estado (Comprometida / Sospechosa / Limpia / Deshabilitada) | Observación |
|---|---|---|---|---|---|
| | Usuario estándar | | | | |
| | Administrador | | | | |
| | Cuenta de servicio | | | | |

---

## Red y servicios

| Origen | Destino | Puerto / Protocolo | Servicio | Dirección (entrante/saliente/lateral) | Observación |
|---|---|---|---|---|---|
| | | | | | |

---

## Alcance confirmado

- Activos afectados (nº y lista):
- Usuarios afectados (nº y lista):
- Servicios afectados:
- Datos afectados (tipo y clasificación: público / interno / confidencial / datos personales):
- Alcance temporal (primer y último evento confirmado):
- Alcance geográfico / sedes:
- Alcance de red (VLANs, segmentos, dominios):

> Si hay datos personales afectados, valorar obligaciones de notificación (RGPD: 72 h a la autoridad de control desde que se tiene constancia). Escalar a DPO / legal.

---

## Alcance descartado

| Elemento revisado | Método de revisión (búsqueda SIEM, EDR, logs) | Resultado | Evidencia |
|---|---|---|---|
| | | | |

---

## Preguntas para cerrar el alcance

- ¿Se ha buscado el mismo IOC (IP, hash, dominio, usuario) en **todo** el parque, no solo en el host de la alerta?
- ¿Se ha ampliado la ventana temporal antes y después del primer evento (mínimo ±24-72 h)?
- ¿Hay hosts o cuentas con la misma vulnerabilidad / configuración expuesta?
- ¿Faltan fuentes de log que impidan confirmar o descartar alcance? Documentarlo como limitación.
