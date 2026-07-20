# Amcor DTO – Claude Plugins

Marketplace privado de plugins de Claude Code para la Digital Transformation Office (DTO) de Amcor.

## Plugins disponibles

### `dto-tools`
Cuatro skills para el ciclo de trabajo del DTO:

- **problem-definition** — entrevista estructurada para definir un problema de negocio (evidence-based, cause-free, solution-free) antes de proponer solución.
- **demand-intake** — registra una demanda nueva, la redacta en formato corporativo y genera un PDF con marca Amcor.
- **change-readiness-assessment** — evalúa la preparación de un equipo frente a un cambio usando el framework ADKAR, con scoring y reporte PDF.
- **projects-list** — lee la base de Notion compartida del DTO y genera un listado simple de demandas (título, fecha de creación, owner, status y descripción de una línea).

### `lss-green-belt`
Skills para el ciclo de trabajo de Lean Six Sigma Green Belt (DMAIC):

- **gb-coach** — Master Black Belt virtual que hace de mentor: revisa en formato tollgate si el approach del candidato en cada fase DMAIC (Define/Measure/Analyze/Improve/Control) es sólido antes de avanzar, con veredicto Go / Go con condiciones / No-Go.
- **define-charter** — arma el project charter de la fase Define: problema, alcance, VOC/CTQs, SIPOC, equipo y business case, con reporte PDF con marca Amcor.
- **analyze-root-cause** — entrevista estructurada de causa raíz (5 Whys / Ishikawa / Pareto) y recomienda qué test estadístico usar según el tipo de dato (t-test, ANOVA, chi-cuadrado, etc.).

## Instalación

```
/plugin marketplace add drotondi/claude-plugins
/plugin install dto-tools@amcor-dto-marketplace
/plugin install lss-green-belt@amcor-dto-marketplace
```

## Actualizar el plugin

Después de modificar algo en `dto-tools/`, subí un bump de versión en `dto-tools/.claude-plugin/plugin.json` y en `marketplace.json`, y hacé push. Los usuarios que ya lo instalaron reciben la actualización en su próxima sesión.
