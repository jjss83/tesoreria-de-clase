# Arquitectura

## Vista general
Fuentes (CSV/Excel) ↔ **Sincronizador** ↔ **SQLite**
→ **Capa de servicios** (CLI/REST con FastAPI)
→ **MCP Server** (herramientas)
→ **Agente** (LLM) que extrae, valida, invoca y responde en Markdown.

## Flujo “pegar mensaje de pago”
1) Usuario pega texto de confirmación → Agente aplica extracción (JSON Schema).  
2) Agente valida (fecha, monto, nombres con fuzzy).  
3) Agente llama MCP `record_payment` → servicios → DB.  
4) Servicios aplican **reglas de asignación** (antigüedad → eventos).  
5) Respuesta con allocations, saldos y enlaces a reportes.

## Estructura de repo (sugerida)
```
/app
  /core        # modelos, reglas de negocio, asignación
  /infra       # adapters csv/excel/sqlite
  /services    # CLI/REST
  /mcp         # server MCP + schemas
  /reports     # plantillas md
/tests
/data          # csv/excel de trabajo
/scripts       # utilidades
```
