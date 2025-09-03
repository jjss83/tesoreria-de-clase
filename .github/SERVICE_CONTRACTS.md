# Contratos de Servicio (REST/CLI) y Asignación

## Endpoints REST (FastAPI, propuesta)
- `POST /payments`
  - Body: `{ date: 'YYYY-MM-DD', amount_crc: number, payer_name: string, students?: string[], method?: string, note?: string, raw_message?: string }`
  - Respuesta: `{ payment_id, allocations: [{charge_id, amount}], unapplied?: number }`
- `POST /charges/generate-monthlies`
  - Body: `{ year: 2025, groups: ['2A','2B'] }` → crea 10 cargos (feb–nov) por estudiante.
- `POST /charges/events`
  - Body: `{ code, name, amount, date, targets: ['student_id'|'group'|'all'] }`
- `GET /reports/debtors?min_paid=7`
- `GET /reports/event?code=DOS_PINOS`
- `GET /reports/summary`
- `GET /students/{id}/statement`

> **CLI**: comandos equivalentes (`record_payment`, `generate_monthlies`, `create_event`, `report_debtors`, etc.)

## JSON Schema — extracción de pagos (para el agente)
```json
{
  "type": "object",
  "required": ["date", "amount_crc", "payer_name"],
  "properties": {
    "date": { "type": "string", "description": "YYYY-MM-DD" },
    "amount_crc": { "type": "number" },
    "payer_name": { "type": "string" },
    "students": { "type": "array", "items": { "type": "string" } },
    "method": { "type": "string" },
    "note": { "type": "string" }
  }
}
```

## Reglas de asignación (default)
- Ordena cargos pendientes por **fecha de vencimiento ascendente** (mensuales), luego **eventos**.
- Distribuye `amount_crc` hasta agotarlo; crea `allocations` por cargo.
- Si hay remanente no asignado → `unapplied` (saldo a favor) o requiere confirmación manual.

## Idempotencia
- Calcular `raw_hash = sha256(normalize(raw_message || (date,payer,amount)))`.
- Si existe un `payment` con el mismo `raw_hash` → no duplicar, retornar el existente.
