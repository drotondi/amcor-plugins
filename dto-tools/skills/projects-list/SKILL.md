---
name: projects-list
description: >
  Use this skill when a user wants an overview, status update, or simple list of the business demands/requirements already registered for Amcor's Digital Transformation Office (DTO). Trigger on phrases like "lista de proyectos", "projects list", "resumen de demandas", "estado de las demandas", "qué demandas tenemos", "dame un listado de las demandas", or any request to see what's been captured via demand intake. Reads the shared Notion database and produces a simple scannable list: title, creation date, owner, status, and a one-line description per demand.
---

# Projects List

Read every demand registered in the shared "DTO - Demandas" Notion database (populated by the `demand-intake` skill) and produce a simple, scannable list — one row per demand, not a long-form summary.

## Workflow

### Step 1: Find and query the database

Read `references/notion_schema.md` in this skill directory for the exact database name and property schema — it's the same database `demand-intake` writes to.

Use `notion-search` or `notion-fetch` to locate the "DTO - Demandas" database. If it can't be found, tell the user no demands have been registered yet and suggest using the demand intake skill first — don't fabricate placeholder projects.

Use `notion-query-data-sources` (or `notion-query-database-view`) to pull all rows. If the user's request implies a filter — a specific requester, sponsor, status, or type ("las demandas de Fulano", "las que están en desarrollo") — apply that filter in the query rather than pulling everything and filtering in prose.

### Step 2: Build the simple list

Present the result as a compact table (Markdown table in chat) with exactly these columns, in this order:

| Título | Fecha de creación | Owner | Status | Descripción |
|---|---|---|---|---|

- **Título**: Nombre del requerimiento (include the ID in parentheses, e.g. "Automatización de facturación (DTO-2026-003)").
- **Fecha de creación**: the Fecha property, as-is.
- **Owner**: the Solicitado por property.
- **Status**: the Estado property.
- **Descripción**: a single line (one short sentence, not a paragraph) synthesizing what the demand is about — distill it from Problema and Necesidad, don't just paste the full polished text from Notion.

One row per demand. Sort by Fecha de creación, most recent first, unless the user asks for a different order.

### Step 3: Offer a document if useful

If the user asks for something to share (a deck, a doc) or the list is long (15+), offer to also produce a Word or PDF version — but default to an inline chat table for a normal-sized list. Don't create a file unless asked or unless the volume clearly warrants it.

## Notes

- This skill is read-only against Notion — it never creates, edits, or deletes demand records. Status changes belong to whatever process the DTO uses to manage the Notion database directly (or a future skill), not this one.
- If the Notion connector isn't available or the query fails, say so plainly rather than presenting stale or invented data.
- Keep the description column to one line per row — if the user wants more depth on a specific demand, offer to expand on that one row rather than lengthening the whole table.
- Language: respond in the language the user is asking in, regardless of what language individual Notion records were written in.
