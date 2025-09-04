# PRD — CajaChica (2º grado)

**Fecha:** 2025-09-03

## 1. Objetivo y alcance

Construir un sistema contable local‑first para:

- Registrar **cuotas** mensuales (feb–nov, ₡8.500 c/u).
- Registrar **cargos extraordinarios** por evento (p. ej., Dos Pinos, Itarar, Día del Niño).
- Aceptar **pagos libres** (monto/fecha cualquieras), incluso para múltiples estudiantes.
- **Conciliar** pagos con cargos con trazabilidad total.
- Generar **reportes** (deudores, eventos, resumen, estados por estudiante).
- Operar **offline** con **CSV/Excel** y espejo en **SQLite**.

## 2. Roles

- **Administrador/contador**: crea cargos, ingresa pagos, genera reportes, exporta.

## 3. Glosario

- **Cargo**: obligación económica (mensual o evento) por estudiante.
- **Pago**: abono recibido (monto libre, puede cubrir varios estudiantes).
- **Asignación** (*allocation*): distribución de un pago a cargos.
- **Saldo**: cargos − pagos aplicados.
- **Pago designado (evento)**: pago cuya intención explícita es cubrir un evento específico; se considera de fondos restringidos y solo puede asignarse a cargos de ese evento.

## 4. Reglas de negocio

1. **Cuotas:** 10 por año, **febrero–noviembre**, ₡8.500 c/u.
2. **Eventos:** monto definido por evento; pueden ser opcionales o específicos por estudiante.
3. **Pagos parciales:** cualquier monto/fecha; pueden cubrir múltiples estudiantes.
4. **Prioridad de asignación:**  
  **Pagos generales (sin designación):** se aplican a cargos pendientes por antigüedad (cuotas) y luego a eventos.  
  **Pagos designados a evento:** se asignan exclusivamente al evento indicado y no reducen cuotas ni otros cargos. Ejemplo: si un responsable debe 5 cuotas y realiza un pago de ₡15.000 para una gira educativa, sigue debiendo 5 cuotas; el pago solo impacta el cargo del evento.
5. **Estados de cargo:** `pendiente | parcial | pagado`.
6. **Moneda:** CRC con dos decimales.

### Planilla Entradas (Excel/CSV)

- Columnas por mes (`FEB…NOV`) representan el **mes de registro del pago**, no necesariamente el periodo del cargo.  
- Columnas de **evento** (p. ej., `Gira Educativa Itarar`, `Gira Educativa dos pinos`) representan pagos **designados** a ese evento.  
- Las columnas `Canceladas` y `Pendientes` son **derivadas** y se calculan:  
  - `canceladas = monto_aplicado_a_cuotas / 8,500`  
  - `pendientes = max(10 − canceladas, 0)`  
  - Se pueden mostrar como decimales (p. ej., `7.8` cuotas).  
- Filas especiales sin estudiante (p. ej., `Devolucion / sobrante de primer grado`) se tratan como **ingresos generales** no asignados a estudiante.

### Planilla Salidas (Excel/CSV)

- Columnas por mes y por evento; una columna `YEAR` suma el total anual.  
- Las filas son **gastos** con `descripcion` (p. ej., `Fiesta medio año`, `Actividad del día del niño`).  
- Puede haber filas de agregación (p. ej., `Total de Gastos`) y celdas de **Saldo** al pie; el sistema debe recalcularlos.

## 5. Modelo de datos mínimo

- **students**: `id, full_name, group, whatsapp?`
- **charges**: `id, student_id, type[monthly|event], period_or_event, amount, description, status`
- **payments**: `id, date, payer_name, method, amount, note, raw_message_id, designation_type[general|event], designation_ref`  
  - `designation_type`: si el pago es de uso general o está designado a un evento.  
  - `designation_ref`: referencia cuando `designation_type=event` (p. ej., `event_code`).
- **allocations**: `id, payment_id, charge_id, amount`
- **events** (opcional): `code, name, amount_default, date`
- **expenses**: `id, date, description, amount, category, event_code?`

## 6. Casos de uso

- **CU1**: Generar cargos mensuales para una lista de estudiantes.
- **CU2**: Crear/editar cargos de evento (global o por estudiante).
- **CU3**: Registrar pago (formulario o texto pegado → extracción), incluyendo designación de evento cuando aplique.
- **CU4**: Conciliar automáticamente respetando la designación de pagos (con ajuste manual opcional).
- **CU5**: Reportes (deudores por umbral, eventos impagos, resumen global, estado de cuenta).
- **CU6**: Exportar a Markdown (y PDF opcional).
- **CU7**: Auditoría (logs).
- **CU8**: Importar planillas de **Entradas** y **Salidas** desde Excel/CSV con mapeo de columnas (meses/eventos) y normalización de montos (`CRC 1,234.56`).
- **CU9**: Calcular `Canceladas` y `Pendientes` por estudiante; generar `Total de Gastos` y `Saldo` global y por evento.

## Mapeo Excel/CSV → Modelo interno

- Entradas (`Numero de Whatsapp, Seccion, Nombre de Estudiante, Canceladas, Pendientes, FEB, MAR, …, eventos, …, DEC`):
  - `Numero de Whatsapp` → `students.whatsapp` (opcional).  
  - `Seccion` → `students.group`.  
  - `Nombre de Estudiante` → `students.full_name` (si coincide con catálogo, se referencia por `id`).  
  - Columnas de mes (`FEB…NOV`, y otras como `DEC`) → crean `payments` con `date` en el mes correspondiente; si no hay designación, `designation_type=general` y se asignan por regla de prioridad.  
  - Columnas de evento (p. ej., `Gira Educativa Itarar`, `Gira Educativa dos pinos`) → crean `payments` con `designation_type=event` y `designation_ref=event_code` mapeado por nombre de columna.  
  - Filas sin estudiante conocido (p. ej., `Devolucion / sobrante de primer grado`) → `payments` de tipo general con `payer_name` descriptivo; no generan `allocations` automáticas.
- Salidas (`Descripcion, FEB, MAR, …, eventos, …, YEAR`):
  - Cada celda con monto crea un `expense` con `date` en el mes/columna y `description` desde la fila.  
  - Si la columna es de evento, se asocia `event_code` para mantener fondos restringidos.  
  - `YEAR` se recalcula desde el sistema; las filas de `Total de Gastos` y `Saldo` son generadas por reporte.

### Notas de parsing

- Montos como `CRC 615,000.00` deben normalizarse quitando prefijo `CRC` y separadores de miles (`,`) respetando punto decimal.  
- Celdas vacías o `CRC 0.00` se tratan como `0`.  
- Encabezados de eventos pueden variar por año; se requiere un catálogo `events` con `code`, `name` y mapeo a encabezado.

## 7. Requisitos no funcionales

- Operación **local** completa.
- Logs legibles + ids determinísticos cuando aplique.
- **Idempotencia** para re‑procesar mensajes (hash del texto).
- Pruebas unitarias e integración.
- Consultas < 200 ms en datasets pequeños.

## 8. Métricas de éxito

- 100% cargos correctos.
- Saldos coinciden con la planilla manual en pruebas.
- Registro de pago desde texto ≤ 30 s.
- Cero duplicados tras reintentos.

## 9. Riesgos

- Ambigüedad en mensajes → plantillas/validaciones.
- Variantes en nombres → catálogo + *fuzzy matching* con confirmación.
- Formatos distintos en CSV/Excel → normalización.
