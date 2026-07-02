# Anomalía geográfica de inicio de sesión

## Objetivo

Investigar accesos desde ubicaciones geográficas anómalas, incompatibles o no habituales para una cuenta.

---

## Datos

| Campo | Valor |
|---|---|
| Usuario | |
| Ubicación habitual | |
| Nueva ubicación | |
| IP origen | |
| ASN / proveedor | |
| Servicio | |
| Login correcto | |
| MFA | |

---

## Evidencias geográficas

| Timestamp | Usuario | IP | País / Ciudad | ASN | Resultado |
|---|---|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿La ubicación es realmente anómala?
- ¿Puede explicarse por VPN, proxy, roaming o proveedor cloud?
- ¿Hay dos ubicaciones incompatibles temporalmente?
- ¿Hubo actividad posterior sensible?
- ¿La cuenta es privilegiada?
- ¿Debe revocarse sesión?

---

## Veredicto

- [ ] Anomalía legítima
- [ ] Uso de VPN/proxy autorizado
- [ ] Toma de cuenta sospechosa
- [ ] Toma de cuenta confirmada
- [ ] Falso positivo
