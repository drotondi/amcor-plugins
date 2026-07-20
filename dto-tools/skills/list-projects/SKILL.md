---
name: list-projects
description: >
  Use this skill when a user wants an executive summary or portfolio-level table of the business demands/requirements already registered for Amcor's Digital Transformation Office (DTO) — trigger on phrases like "resumen ejecutivo del portfolio", "list-projects", "dame un resumen ejecutivo de las demandas", "tabla de proyectos", "portfolio de demandas", or any request for a director-level, one-row-per-initiative view of what's been captured via demand intake. Reads the shared Notion database and produces a single table (ID, Iniciativa, Estado, Descripción) — one tightly compressed line per demand.
---

# List Projects

Read every demand registered in the shared "DTO - Demandas" Notion database (populated by the `demand-intake` skill) and produce one portfolio-level executive-summary table — one row per initiative, scannable by a director in a single pass.

## Workflow

### Step 1: Find and query the database

Read `references/notion_schema.md` in this skill directory for the exact database name and property schema — it's the same database `demand-intake` writes to.

Use `notion-search` or `notion-fetch` to locate the "DTO - Demandas" database. If it can't be found, tell the user no demands have been registered yet and suggest using the demand intake skill first — don't fabricate placeholder projects.

Use `notion-query-data-sources` (or `notion-query-database-view`) to pull all rows. If the user's request implies a filter — a specific requester, sponsor, status, or type ("las demandas de Fulano", "las que están en desarrollo") — apply that filter in the query rather than pulling everything and filtering in prose.

### Step 2: Build the executive-summary table

Generate one table listing every demand, one row per initiative. Columns, in this order:

| ID | Iniciativa | Estado | Descripción |
|---|---|---|---|

- **ID**: the ID property (e.g. `DTO-2026-003`).
- **Iniciativa**: Nombre del requerimiento.
- **Estado**: the Estado property, as-is.
- **Descripción**: a single, tightly compressed line (max ~1 sentence, no line breaks) synthesizing in your own words what problem it solves and the expected benefit/goal — pull from Problema, Necesidad, Alcance, Beneficios, and Meta, but compress hard, don't list each field. Ground every word in what those fields actually say — never invent a benefit or scope detail that isn't there. If a field is missing or "No definido aún", let the sentence reflect that gap plainly (e.g. "...aunque todavía sin meta numérica definida") rather than papering over it.

Keep each demand's summary short enough that a director can scan 10+ of them in one pass — this is a portfolio view, not the full intake report (that's what the PDF from `demand-intake` is for). One row per demand, no extra commentary between rows.

Sort by ID (which sorts chronologically by year and sequence) unless the user asks for a different order (e.g. grouped by Estado).

### Step 3: Add a brief portfolio note (optional, only if useful)

If the table is long (10+) or the user's request suggests they want more than the raw table, add one short closing line with the total count and a breakdown by Estado — nothing longer than that. Skip this entirely for a short, straightforward request; the table is the deliverable, not a preamble to it.

### Step 4: Offer a document if useful

If the user asks for something to share (a deck, a doc) or the table is long (15+), offer to also produce a Word or PDF version — but default to an inline chat table for a normal-sized portfolio. Don't create a file unless asked or unless the volume clearly warrants it.

## Notes

- This skill is read-only against Notion — it never creates, edits, or deletes demand records.
- If the Notion connector isn't available or the query fails, say so plainly rather than presenting stale or invented data.
- This skill is distinct from `projects-list`: `projects-list` gives a simple per-demand list (título, fecha de creación, owner, status, descripción); `list-projects` gives a portfolio executive-summary table (ID, iniciativa, estado, descripción compressed to a single synthesized sentence). Use whichever the user's phrasing points to; if ambiguous, ask which format they want.
- Language: respond in the language the user is asking in, regardless of what language individual Notion records were written in.
