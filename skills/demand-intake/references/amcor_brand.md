# Amcor brand spec (condensed, for PDF reports)

Source of truth: Amcor Brand Guidelines 2026. Use these values exactly — do not invent colors or adjust the palette.

## Colors (hex)

| Role | Hex | Use |
|---|---|---|
| Amcor Dark Blue | `#00395A` | Dominant. Header bar, section titles, dominant surface. |
| Amcor White | `#FFFFFF` | Page background, text on dark. |
| Amcor Light Blue | `#00A1DE` | Accent — field labels, thin rules, highlights. |
| Amcor Green | `#00A551` | Optional accent for positive/benefit sections only. |
| Black (functional) | `#000000` | Body text only. Never as a brand color. |

Dark Blue must dominate the layout. Light Blue and Green are accents only — never more than a thin rule, a label color, or a small icon/box.

## Typography

- Use **Arial** (Bold for headings, Regular for body) — this is the approved digital fallback and the safe choice for PDF generation with reportlab, since AmcorPro may not be embedded.
- Headings: Arial Bold, Dark Blue (or White if on a Dark Blue band).
- Body: Arial Regular, Black or Dark Blue, ~10-11pt.
- Field labels (e.g. "Solicitado por:"): Arial Bold, small caps or sentence case, Light Blue or Dark Blue.
- Sentence case for section headers and body content. Avoid ALL CAPS except very short labels.

## Report layout for demand_intake PDF

This layout follows a bordered form/grid style (like an internal corporate intake form), not a flowing-prose report. Every section is a bordered table cell — visible grid lines throughout, Dark Blue for lines and labels, white background, black value text.

1. **Masthead** (no colored band, white background, thin Dark Blue rule underneath): word "AMCOR" as a wordmark, bold, Dark Blue, top-left — plain text is fine, no logo image. To its right/center: "Digital Transformation Office" as a subtitle line. Below that, in bold: the requirement name followed by the request ID, e.g. "**Automatización de reporte de tracking — DTO-2026-003**".
2. **Info grid**: a bordered table, 3 rows × 2 columns, every cell with a thin Dark Blue border. Each cell contains a label (Dark Blue Arial Bold, small, on its own line) directly above its value (Black Arial Regular):
   - Row 1: Proceso de negocio | Sponsor
   - Row 2: Solicitado por | Líder de IT
   - Row 3: Tipo de requerimiento | Fecha
3. **Requirement name banner**: a full-width single-cell table row, filled Dark Blue, white Arial Bold text: "Nombre del requerimiento: {value}".
4. **Body grid**: a bordered table, 3 rows × 2 columns, matching the 6 body questions in pairs, each cell bordered like the info grid. Question text as a bold Dark Blue mini-header inside the cell, the polished paragraph as black body text below it, within the same cell:
   - Row 1: ¿Cuál es el problema que se quiere resolver? | ¿Cuál es la necesidad?
   - Row 2: ¿Cuál es el alcance? | ¿Cuáles son los beneficios esperables?
   - Row 3: ¿Qué impactos/riesgos tiene el negocio hoy? | ¿Cuál sería la meta que se desea alcanzar?
5. **Footer**: small Dark Blue rule at the bottom of each page with "Amcor — Digital Transformation Office" and the generation date in small gray/Dark Blue text.
6. One page is fine for typical content; let text reflow to a second page naturally (repeat only the footer, not the masthead, on continuation pages). If a body cell's polished text is long, let that row grow taller rather than shrinking the font below ~9.5pt.

Do not use the earlier "solid Dark Blue header band + flowing prose sections" style — this bordered grid/form style replaces it.

## reportlab notes

- Use `platypus` (`SimpleDocTemplate`, `Paragraph`, `Table`, `Spacer`, `TableStyle`) rather than raw canvas, so text reflows properly across pages and cells resize with content.
- Define colors with `from reportlab.lib.colors import HexColor` and reuse `HexColor("#00395A")`, etc. — never approximate with named colors.
- Build both the info grid and body grid as `Table` objects whose cell contents are `Paragraph` flowables (not raw strings), so long answers wrap and grow the row height instead of overflowing.
- Apply `TableStyle` with `GRID` (thin, `HexColor("#00395A")`, 0.5pt) around every cell in both grids, `VALIGN` top, and modest cell padding (~6pt) so text doesn't touch the borders.
- For the requirement-name banner, use a single-row, single-column `Table` with `BACKGROUND` Dark Blue and white bold text, spanning the full page width.
- Do not use Unicode subscript/superscript characters; use reportlab's `<sub>`/`<super>` tags if ever needed.
