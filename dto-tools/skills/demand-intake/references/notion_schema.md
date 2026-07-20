# Notion schema — "DTO - Demandas" database

This is the single shared database that backs both the `demand-intake` skill (writes) and the `projects-list` skill (reads). Both skills must agree on this exact name and property set — do not create a second database with a similar name.

**Database name (Notion page title):** `DTO - Demandas`

## Properties

| Property name | Type | Notes |
|---|---|---|
| Nombre del requerimiento | Title | The requirement name — this is the database's title property |
| ID | Rich text | e.g. `DTO-2026-001` |
| Fecha | Date | Intake date |
| Idioma | Rich text | e.g. `es`, `en`, `pt` |
| Proceso de negocio | Rich text | |
| Solicitado por | Rich text | |
| Tipo de requerimiento | Select | Options: `Nuevo proceso`, `Nueva funcionalidad`, `Mejora existente` |
| Sponsor | Rich text | |
| Líder de IT | Rich text | |
| Problema | Rich text | Polished (Step 2) version |
| Necesidad | Rich text | Polished version |
| Alcance | Rich text | Polished version |
| Beneficios | Rich text | Polished version |
| Impactos y riesgos | Rich text | Polished version |
| Meta | Rich text | Polished version |
| Estado | Select | Options: `Nueva`, `En análisis`, `En desarrollo`, `Completada`, `Descartada` — default to `Nueva` on creation; `projects-list` reads this but does not write it |

## Creating the database (if it doesn't exist)

Use `notion-create-database` with SQL DDL syntax (per the Notion MCP tool's own instructions) to create a database with the title `DTO - Demandas` and the properties above, in whatever Notion workspace/parent page the connected integration has access to. If unsure which parent page to use, ask the user once where they'd like the database created (e.g. a "DTO" or "Digital Transformation Office" page/teamspace), then remember that location isn't something this skill can infer — future runs will find it via `notion-search` by name.

## Querying

- `demand-intake` queries only to count existing IDs for the current year (to assign the next sequential number).
- `projects-list` queries the full database to build executive summaries — see that skill's SKILL.md.
- `list-projects` queries the full database to build a lighter-weight portfolio table (no overview section) — see that skill's SKILL.md.
