# Sospecha de exfiltración de datos

## Objetivo

Investigar transferencia anómala de datos hacia destinos no habituales.

---

## Datos

| Campo | Valor |
|---|---|
| Host origen | |
| Usuario | |
| Destino | |
| Volumen | |
| Protocolo | |
| Servicio | |
| Timestamp | |

---

## Evidencias

| Timestamp | Origen | Destino | Protocolo | Volumen | Observación |
|---|---|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿El volumen es anómalo para ese host/usuario?
- ¿El destino es conocido?
- ¿Hay compresión o cifrado previo?
- ¿Hay actividad de malware o C2?
- ¿Se accedió a datos sensibles?
- ¿Debe bloquearse el destino?

---

## Veredicto

- [ ] Transferencia legítima
- [ ] Exfiltración sospechosa
- [ ] Exfiltración confirmada
- [ ] Falso positivo
