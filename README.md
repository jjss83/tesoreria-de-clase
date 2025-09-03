# CajaChica (2º grado) — Local‑First Accounting

**Fecha:** 2025-09-03

Sistema contable ligero para administrar la caja chica del 2º grado (cuotas mensuales y cargos extraordinarios) con operación **local**, almacenamiento en **CSV/Excel/SQLite**, **capa de servicios** (CLI/REST), **MCP server** y **agente** que registra pagos desde texto pegado y genera reportes.

## Módulos
- **Datos**: CSV/Excel ↔ SQLite (sincronización).
- **Servicios**: CLI y/o REST mínimo para casos de uso.
- **MCP**: herramientas para `record_payment`, `generate_report`, `student_statement`, `sync_spreadsheet`.
- **Agente**: extracción estructurada, validación, invocación MCP, respuesta en Markdown.
- **Reportes**: deudores (< umbral de cuotas pagadas), eventos impagos, resumen global, estado por estudiante.

## Archivos de referencia
- [`PRD.md`](./PRD.md): requisitos y reglas de negocio.
- [`ARCHITECTURE.md`](./ARCHITECTURE.md): arquitectura y flujo.
- [`DATA_SCHEMAS.md`](./DATA_SCHEMAS.md): esquemas CSV y SQLite.
- [`SERVICE_CONTRACTS.md`](./SERVICE_CONTRACTS.md): contratos (REST/CLI) y reglas de asignación.
- [`REPORTS.md`](./REPORTS.md): plantillas y criterios de orden.
- [`MCP_AGENT_PROMPT.md`](./MCP_AGENT_PROMPT.md): prompt del agente con MCP.
- [`TEST_PLAN.md`](./TEST_PLAN.md): plan de pruebas y aceptación.
- [`ROADMAP.md`](./ROADMAP.md): plan por sprints.
- [`LOGGING_AUDIT.md`](./LOGGING_AUDIT.md): auditoría e idempotencia.
- [`COPILOT_INSTRUCTIONS.md`](./COPILOT_INSTRUCTIONS.md): guía para GitHub Copilot/Agent.
- [`copilot-instructions.md`](./copilot-instructions.md): instrucciones automáticas para actualización de changelog.
