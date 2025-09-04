# GitHub Copilot / Agent — Instrucciones de Contexto

## Objetivo
Asistir en el desarrollo de un sistema local‑first para la caja chica del 2º grado, manteniendo simplicidad, SOLID y alta testeabilidad.

## Archivos de referencia (mantener actualizados)
- `PRD.md`: reglas y alcance.
- `ARCHITECTURE.md`: decisiones de diseño y flujo.
- `DATA_SCHEMAS.md`: fuente de verdad de esquemas.
- `SERVICE_CONTRACTS.md`: endpoints/CLI y asignación.
- `REPORTS.md`: formatos de salida.
- `MCP_AGENT_PROMPT.md`: contrato con el agente.
- `TEST_PLAN.md`: oráculos de prueba.
- `ROADMAP.md`: orden de trabajo.
- `LOGGING_AUDIT.md`: lineamientos de auditoría.
- `copilot-instructions.md`: instrucciones automáticas para changelog.

## Guía para Copilot
- Sugerir funciones pequeñas y testeables.
- Proponer pruebas al crear lógica de negocio.
- Mantener consistencia con los contratos (no inventar campos).
- Cuando detecte ambigüedad, anotar `// TODO: clarify` y proponer una prueba.
- Preferir *adapters* puros en `infra` y reglas en `core`.
- Al emitir código, referenciar secciones exactas de estos archivos.

## Gestión Automática de Changelog
- **Detectar cambios** en commits y archivos modificados desde la última actualización del changelog.
- **Categorizar automáticamente** según Keep a Changelog: Added, Changed, Fixed, Removed, Security.
- **Enfocar en impacto del usuario** más que en detalles técnicos de implementación.
- **Incluir contexto de tesorería** para cambios relacionados con cálculos financieros, pagos o reportes.
- **Mantener formato profesional** y consistente en todas las entradas del changelog.
