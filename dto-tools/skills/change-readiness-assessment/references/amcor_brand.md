# Amcor brand spec (condensed) + PDF layout for Change Readiness Assessment

## Colors (hex) — same as the rest of the DTO toolkit, don't invent new ones

| Role | Hex | Use |
|---|---|---|
| Amcor Dark Blue | `#00395A` | Dominant. Masthead, section headers, table borders. |
| Amcor White | `#FFFFFF` | Page background, text on dark. |
| Amcor Light Blue | `#00A1DE` | Accent — bar chart fill, thin rules. |
| Amcor Green | `#00A551` | Use for "Alta preparación" level indicator only. |
| Amber/Gray fallback for "moderada" | `#B8860B` (dark goldenrod) or similar mid-tone — not an official Amcor accent, but there's no approved amber in the palette, so use a muted gray-brown, never red/green traffic-light colors that aren't in the brand. | "Preparación moderada" level indicator. |
| Amcor Dark Blue (darker tint) | `#001F30` or plain Dark Blue | "Baja preparación" level indicator — use Dark Blue itself rather than inventing a red; pair with bold text saying "riesgo alto" so the message doesn't depend on color alone. |
| Black (functional) | `#000000` | Body text. |

Keep Dark Blue dominant throughout, same as the demand-intake PDF.

## Typography

Same as the rest of the toolkit: Arial/Helvetica, Bold for headings and labels, Regular for body, ~9.5-11pt body text.

## PDF structure

1. **Masthead** (plain text, no logo image, matching the demand-intake style): "AMCOR" wordmark bold Dark Blue top-left, "Digital Transformation Office — Change Readiness Assessment" as subtitle, then below in bold: the change/iniciativa name and the team or stakeholder evaluated, e.g. "**Migración ERP LATAM — Equipo: Logística Regional**". Thin Dark Blue rule underneath.
2. **Respondent info block**: small bordered table with Nombre, Función/rol, Área, Fecha, and whether the target is a Team or a Stakeholder plus its name.
3. **Results summary**: a bordered table — one row per ADKAR dimension with columns Dimensión / Puntaje / % / Nivel — plus a Total row. Next to or below it, a simple horizontal bar per dimension: a thin table row per dimension where a `Table` cell's background is Light Blue filled proportionally to the percentage (e.g. build it as a 100-unit-wide table split into a colored cell of width = percentage and a white/empty cell for the remainder) — this avoids needing `reportlab.graphics` and keeps it simple and reliable.
4. **Barrier point callout**: a full-width Dark Blue banner (same style as the demand-intake requirement-name banner) with white bold text naming the barrier point dimension (or the lowest-scoring one if none crosses the 60% threshold), followed by a paragraph (black text on white, right below the banner) with the consultant's interpretation and recommendation — see `scoring.md` for what this should say.
5. **Acciones sugeridas**: a section (Dark Blue bold section header "Acciones sugeridas") right after the barrier-point callout, with one sub-block per dimension that scored below 80% — barrier point dimension first. Each sub-block: dimension name in bold Dark Blue, then 2-4 short bullet points (black text) with the recommended actions from Step 4. See `recommendations.md` for the content bank.
6. **Detailed answers**: one section per dimension (Dark Blue bold section header), listing each question with its answer (Sí/Parcial/No) and, for "No" answers, the follow-up note if one was captured. A simple two-column layout works: question text (regular) then the answer in bold Dark Blue right after it, e.g. "1. ¿...? — **No** (nota: ...)".
7. **Footer**: same as the rest of the toolkit — thin Dark Blue rule, "Amcor — Digital Transformation Office", generation date.

## reportlab notes

- Use `platypus` (`SimpleDocTemplate`, `Table`, `TableStyle`, `Paragraph`, `Spacer`) — consistent with the rest of the plugin's PDFs.
- For the proportional bars, build each as a 1-row `Table` with two cells whose `colWidths` are `[total_width * pct/100, total_width * (100-pct)/100]`, `BACKGROUND` Light Blue and White respectively, no visible border needed on that inner table (or a thin Dark Blue outline around the whole bar for definition).
- Reuse `HexColor` for every color — never approximate with named colors.
- Let the detailed-answers section flow across pages naturally; don't try to force everything onto one page.
