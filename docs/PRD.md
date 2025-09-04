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

## 5. Modelo de datos mínimo

- **students**: `id, full_name, group`
- **charges**: `id, student_id, type[monthly|event], period_or_event, amount, description, status`
- **payments**: `id, date, payer_name, method, amount, note, raw_message_id, designation_type[general|event], designation_ref`  
  - `designation_type`: si el pago es de uso general o está designado a un evento.  
  - `designation_ref`: referencia cuando `designation_type=event` (p. ej., `event_code`).
- **allocations**: `id, payment_id, charge_id, amount`
- **events** (opcional): `code, name, amount_default, date`

## 6. Casos de uso

- **CU1**: Generar cargos mensuales para una lista de estudiantes.
- **CU2**: Crear/editar cargos de evento (global o por estudiante).
- **CU3**: Registrar pago (formulario o texto pegado → extracción), incluyendo designación de evento cuando aplique.
- **CU4**: Conciliar automáticamente respetando la designación de pagos (con ajuste manual opcional).
- **CU5**: Reportes (deudores por umbral, eventos impagos, resumen global, estado de cuenta).
- **CU6**: Exportar a Markdown (y PDF opcional).
- **CU7**: Auditoría (logs).

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
