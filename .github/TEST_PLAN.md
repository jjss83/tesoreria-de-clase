# Plan de Pruebas

## Niveles
- **Unidad**: reglas de asignación, normalización de montos, formateo de reportes.
- **Integración**: CSV/Excel ↔ SQLite, endpoints REST, CLI.
- **End‑to‑End**: flujo agente → MCP → servicios → DB → reporte.

## Casos de prueba clave
1. Pago exacto de 3 cuotas en un abono.
2. Pago parcial que cubre 1 cuota + parte de evento.
3. Nombre similar (fuzzy) requiere confirmación y no duplica registros.
4. Reporte “< 7 cuotas pagadas” vs “eventos impagos”.
5. Re‑proceso del mismo mensaje no duplica (`raw_hash`).

## Criterios de aceptación
- Resultados reproducibles en CLI/REST.
- Exportes Markdown con orden alfabético estable.
