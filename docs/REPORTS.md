# Reportes y Plantillas Markdown

## Criterios generales
- Orden **alfabético por apellido** del estudiante (o `full_name` normalizado).
- Montos con dos decimales y separador de miles donde aplique, p. ej.: `8,500.00`.
- Para cuotas pagadas/pendientes: formato `n (8,500.00)` cuando se pida.

## Reporte: Deudores (umbral de cuotas pagadas)
Campos:
- `Estudiante`, `Grupo`, `Cuotas pagadas`, `Cuotas pendientes`, `Monto pendiente`

## Reporte: Eventos impagos (por código)
Campos:
- `Estudiante`, `Grupo`, `Evento`, `Estado` (`pendiente|parcial`), `Monto pendiente`

## Reporte: Resumen global
Campos:
- `Entradas (pagos)`, `Salidas (gastos) [opcional]`, `Saldo`

## Estado de cuenta por estudiante
Campos:
- `Cargos` (lista con estado), `Pagos` (lista), `Saldo`.

> Exportar como `.md` y opcionalmente a PDF.
