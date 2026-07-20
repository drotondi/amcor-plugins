# Amcor brand spec (condensed, for the Project Charter PDF)

Source of truth: Amcor Brand Guidelines 2026. Use these values exactly — do not invent colors or adjust the palette.

## Colors (hex)

| Role | Hex | Use |
|---|---|---|
| Amcor Dark Blue | `#00395A` | Dominant. Header bar, section titles, table headers, dominant surface. |
| Amcor White | `#FFFFFF` | Page background, text on dark. |
| Amcor Light Blue | `#00A1DE` | Accent — field labels, thin rules, SIPOC column headers. |
| Amcor Green | `#00A551` | Optional accent — goal/target values only, never a whole section. |
| Black (functional) | `#000000` | Body text only. Never as a brand color. |

Dark Blue must dominate the layout. Light Blue and Green are accents only — never more than a thin rule, a label color, or a small header band.

## Typography

- Use **Arial** (Bold for headings, Regular for body) — approved digital fallback, safe for reportlab.
- Headings: Arial Bold, Dark Blue (or White if on a Dark Blue band).
- Body: Arial Regular, Black or Dark Blue, ~10-11pt.
- Field labels: Arial Bold, sentence case, Light Blue or Dark Blue.
- Sentence case throughout. Avoid ALL CAPS except very short table headers (e.g. SIPOC column names).

## Report layout for the Project Charter PDF

Bordered form/grid style, consistent with other DTO reports — visible grid lines, Dark Blue for lines/labels, white background, black value text. Multi-page is expected; only the masthead appears on page 1, the footer repeats on every page.

1. **Masthead** (white background, thin Dark Blue rule underneath): "AMCOR" wordmark, bold, Dark Blue, top-left. Subtitle line: "Digital Transformation Office — Lean Six Sigma Green Belt". Below, bold: the project name, e.g. "**Project Charter — Reducción de scrap en línea 3**".
2. **Info grid**: bordered table, 3 rows × 2 columns, thin Dark Blue border per cell, label (Dark Blue Arial Bold, small) above value (Black Arial Regular):
   - Row 1: Green Belt candidato | Sponsor
   - Row 2: Champion / Mentor (MBB) | Fecha de inicio
   - Row 3: Área / proceso | Fecha objetivo de cierre
3. **Problem & goal banner**: full-width single-cell table, filled Dark Blue, white text. Two short paragraphs inside, each with a small white-on-transparent bold label: "Problema:" and "Meta:".
4. **Business case section**: section header ("Business case", Arial Bold Dark Blue) followed by a bordered single-cell table with the polished business-case paragraph (Black body text). If a quantified benefit exists, show it as a short highlighted line in Amcor Green bold just below the paragraph (e.g. "Beneficio estimado: USD 45,000/año").
5. **VOC / CTQ table**: section header "Voz del cliente (VOC) y CTQs". Bordered table, header row filled Light Blue with white bold text: columns "Cliente", "Necesidad (VOC)", "CTQ (Critical to Quality)". One row per VOC/CTQ pair captured (2-4 rows typical). Cell text as `Paragraph` flowables so long text wraps.
6. **SIPOC table**: section header "SIPOC". Bordered 5-column table, header row filled Light Blue with white bold text: "Suppliers", "Inputs", "Process", "Outputs", "Customers". The Process column lists the 4-7 high-level steps as a numbered list inside the cell (one `Paragraph` with `<br/>` between steps); the other four columns list their items the same way. Keep this table landscape-friendly — if content is wide, allow the page to use a wider table (still portrait page, just narrow margins) rather than shrinking the font below 9pt.
7. **Scope section**: section header "Alcance". Two-column bordered table: "Incluye" | "No incluye", each cell a bulleted list built as a `Paragraph` with `<br/>` between items.
8. **Team section**: section header "Equipo del proyecto". Bordered table, one row per member: columns "Nombre", "Rol", "Dedicación / involucramiento" (this last column free text like "Full-time durante el proyecto" or "Consulta puntual").
9. **Footer**: thin Dark Blue rule at the bottom of every page with "Amcor — Digital Transformation Office — LSS Green Belt" and the generation date, small gray/Dark Blue text.

Do not use a flowing-prose-only layout — the grid/table style is what makes this recognizable as a formal charter document, matching the other DTO reports.

## reportlab notes

- Use `platypus` (`SimpleDocTemplate`, `Paragraph`, `Table`, `Spacer`, `TableStyle`), not raw canvas, so tables reflow across pages and cells resize with content.
- Define colors with `from reportlab.lib.colors import HexColor` — reuse `HexColor("#00395A")`, `HexColor("#00A1DE")`, `HexColor("#00A551")`.
- Every table cell containing more than a few words must be a `Paragraph` flowable, not a raw string, so long VOC/CTQ or SIPOC text wraps instead of overflowing.
- Apply `TableStyle` with `GRID` (thin, Dark Blue, 0.5pt), `VALIGN` top, ~6pt cell padding on every bordered table. Header rows (VOC/CTQ, SIPOC) use `BACKGROUND` Light Blue with white bold text.
- The problem & goal banner and any single-row highlight bands use a single-row/column `Table` with `BACKGROUND` Dark Blue spanning the full page width.
- Do not use Unicode subscript/superscript; use reportlab's `<sub>`/`<super>` tags if ever needed.
