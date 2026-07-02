# DNS sospechoso o beaconing C2

## Objetivo

Investigar consultas DNS raras, dominios dinámicos, túnel DNS o conexiones periódicas compatibles con C2.

---

## Datos

| Campo | Valor |
|---|---|
| Host origen | |
| Usuario | |
| Dominio / IP destino | |
| Frecuencia | |
| Proceso asociado | |
| Sensor | |
| Timestamp | |

---

## Evidencias

| Timestamp | Host | Dominio / IP | Frecuencia | Protocolo | Observación |
|---|---|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿El dominio es raro, nuevo o dinámico?
- ¿Hay periodicidad constante?
- ¿Hay subdominios largos o de alta entropía?
- ¿Qué proceso originó la conexión?
- ¿Hay malware o script asociado?
- ¿Más hosts consultan lo mismo?

---

## Contención

- [ ] Bloquear dominio
- [ ] Bloquear IP
- [ ] Aislar host
- [ ] Añadir IOC
- [ ] Revisar tráfico completo
