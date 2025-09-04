# Esquemas de Datos (CSV/Excel y SQLite)

## CSV mínimos

- `students.csv`: `student_id,full_name,group`
- `charges.csv`: `charge_id,student_id,type,period_or_event,amount,status`
- `payments.csv`: `payment_id,date,payer_name,amount,method,note,raw_hash,designation_type,designation_ref`  
  - `designation_type`: `general|event`  
  - `designation_ref`: referencia cuando `designation_type=event` (por ejemplo, `event_code`)
- `allocations.csv`: `allocation_id,payment_id,charge_id,amount`

### Convenciones

- Decimales con punto; miles opcional. Siempre **dos decimales** al exportar.
- Fechas ISO `YYYY-MM-DD`.
- `status` en `charges`: `pending|partial|paid`.

## SQLite (DDL sugerido)

```sql
CREATE TABLE students (
  id TEXT PRIMARY KEY,
  full_name TEXT NOT NULL,
  "group" TEXT NOT NULL
);

CREATE TABLE charges (
  id TEXT PRIMARY KEY,
  student_id TEXT NOT NULL REFERENCES students(id),
  type TEXT CHECK(type IN ('monthly','event')) NOT NULL,
  period_or_event TEXT NOT NULL,
  amount REAL NOT NULL,
  description TEXT,
  status TEXT CHECK(status IN ('pending','partial','paid')) NOT NULL DEFAULT 'pending'
);

CREATE TABLE payments (
  id TEXT PRIMARY KEY,
  date TEXT NOT NULL, -- ISO
  payer_name TEXT NOT NULL,
  method TEXT,
  amount REAL NOT NULL,
  note TEXT,
  raw_message_id TEXT,
  raw_hash TEXT UNIQUE,
  designation_type TEXT CHECK(designation_type IN ('general','event')) DEFAULT 'general',
  designation_ref TEXT
);

CREATE TABLE allocations (
  id TEXT PRIMARY KEY,
  payment_id TEXT NOT NULL REFERENCES payments(id),
  charge_id TEXT NOT NULL REFERENCES charges(id),
  amount REAL NOT NULL
);

```
