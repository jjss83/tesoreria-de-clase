# Auditoría, Logs e Idempotencia

## Logging
- Archivo de texto con nivel INFO/ERROR y timestamps.
- Registrar: acción, payload resumido (sin datos sensibles), resultado/ids.

## Idempotencia
- `raw_hash = sha256(normalize(texto_original || (date,payer,amount)))`.
- Rechazar duplicados devolviendo el registro previo (HTTP 200 con indicador `duplicate: true`).

## Trazabilidad
- Cada `allocation` referencia `payment_id` y `charge_id`.
- Export de auditoría: CSV consolidado de `payments` y `allocations`.
