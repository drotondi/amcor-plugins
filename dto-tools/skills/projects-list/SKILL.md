---
name: projects-list
description: >
  Use this skill when a user wants an overview, status update, or executive summary of the business demands/requirements already registered for Amcor's Digital Transformation Office (DTO). Trigger on phrases like "lista de proyectos", "projects list", "resumen de demandas", "estado de las demandas", "qué demandas tenemos", "dame un resumen ejecutivo de las soluciones", or any request to see what's been captured via demand intake. Reads the shared Notion database and produces one executive summary per demand plus a portfolio-level overview.
---

# Projects List

Read every demand registered in the shared "DTO - Demandas" Notion database (populated by the `demand-intake` skill) and produce an executive summary for each one, plus a short portfolio-level overview.

## Workflow

### Step 1: Find and query the database

Read `references/notion_schema.md` in this skill directory for the exact database name and property schema — it's the same database `demand-intake` writes to.

Use `notion-search` or `notion-fetch` to locate the "DTO - Demandas" database. If it can't be found, tell the user no demands have been registered yet and suggest using the demand intake skill first — don't fabricate placeholder projects.

Use `notion-query-data-sources` (or `notion-query-database-view`) to pull all rows. If the user's request implies a filter — a specific requester, sponsor, status, or type ("las demandas de Fulano", "las que están en desarrollo") — apply that filter in the query rather than pulling everything and filtering in prose.

### Step 2: Build one executive summary per demand

For each row, produce a compact executive summary (not a re-dump of every field) with this shape:

- **Title line**: ID + requirement name + current status (e.g. "**DTO-2026-003 — Automatización de facturación** (En desarrollo)")
- **2-4 sentence summary** synthesizing, in your own words: what problem it solves, what the solution/scope is, and the expected benefit or goal — pull this from Problema, Necesidad, Alcance, Beneficios, and Meta, but compress into a tight paragraph rather than listing each field separately.
- **One line of metadata**: Solicitado por, Sponsor, Líder de IT, Proceso de negocio — as a compact inline line, not a table, unless the user asks for a table.

Keep each demand's summary short enough that a director can scan 10+ of them in one pass — this is a portfolio view, not the full intake report (that's what the PDF from `demand-intake` is for).

### Step 3: Add a portfolio-level overview

Before or after the individual summaries (before is usually better for a director-level audience), add a short overview:
- Total count of demands, and a breakdown by Estado and by Tipo de requerimiento.
- Flag anything notable: demands with no clear goal/metric ("No definido aún" in Meta), demands stalled in the same status a long time (only if a way to detect this is available — e.g. a "last edited" timestamp — otherwise skip rather than guessing), or a business process appearing in multiple demands (possible duplication or a systemic issue worth flagging).

### Step 4: Offer a document if useful

If the user asks for something to share (a deck, a doc) or the list is long (10+), offer to also produce a Word or PDF version — but default to an inline chat response for a normal-sized list. Don't create a file unless asked or unless the volume clearly warrants it.

## Notes

- This skill is read-only against Notion — it never creates, edits, or deletes demand records. Status changes belong to whatever process the DTO uses to manage the Notion database directly (or a future skill), not this one.
- If the Notion connector isn't available or the query fails, say so plainly rather than presenting stale or invented data.
- Language: respond in the language the user is asking in, regardless of what language individual Notion records were written in.
