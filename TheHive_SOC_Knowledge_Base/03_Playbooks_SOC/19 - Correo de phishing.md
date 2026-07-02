# Correo de phishing

## Objetivo

Investigar correo sospechoso, adjuntos maliciosos, URLs fraudulentas o compromiso de cuenta asociado.

---

## Datos

| Campo | Valor |
|---|---|
| Remitente | |
| Destinatario | |
| Asunto | |
| URL | |
| Adjunto | |
| Hash | |
| Timestamp | |

---

## Evidencias

| Timestamp | Remitente | Destinatario | Asunto | IOC | Acción |
|---|---|---|---|---|---|
| | | | | | |

---

## Preguntas

- ¿El remitente es legítimo?
- ¿SPF/DKIM/DMARC son válidos?
- ¿La URL o adjunto es malicioso?
- ¿Alguien hizo clic o abrió el adjunto?
- ¿Hay más destinatarios?
- ¿Hay reglas de buzón o reenvío sospechoso?

---

## Contención

- [ ] Eliminar correo
- [ ] Bloquear URL/dominio
- [ ] Bloquear hash
- [ ] Resetear cuenta si procede
- [ ] Notificar usuarios
