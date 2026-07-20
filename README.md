# Amcor DTO – Claude Plugins

Marketplace privado de plugins de Claude Code para la Digital Transformation Office (DTO) de Amcor.

## Plugins disponibles

### `dto-tools`
Cuatro skills para el ciclo de trabajo del DTO:

- **problem-definition** — entrevista estructurada para definir un problema de negocio (evidence-based, cause-free, solution-free) antes de proponer solución.
- **demand-intake** — registra una demanda nueva, la redacta en formato corporativo y genera un PDF con marca Amcor.
- **change-readiness-assessment** — evalúa la preparación de un equipo frente a un cambio usando el framework ADKAR, con scoring y reporte PDF.
- **projects-list** — lee la base de Notion compartida del DTO y genera un resumen ejecutivo del portfolio de demandas.

## Instalación

```
/plugin marketplace add drotondi/claude-plugins
/plugin install dto-tools@amcor-dto-marketplace
```

## Actualizar el plugin

Después de modificar algo en `dto-tools/`, subí un bump de versión en `dto-tools/.claude-plugin/plugin.json` y en `marketplace.json`, y hacé push. Los usuarios que ya lo instalaron reciben la actualización en su próxima sesión.
