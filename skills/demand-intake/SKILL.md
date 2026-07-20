---
name: demand-intake
description: >
  Use this skill when a user wants to register, log, or document a new business demand or requirement for the Digital Transformation Office (DTO) at Amcor. Trigger on phrases like "nueva demanda", "registrar una demanda", "quiero levantar un requerimiento", "demand intake", "necesito documentar un pedido", or any request to capture what a colleague needs so the DTO can understand what kind of solution to provide. Walks the user through a structured set of questions about the requirement, polishes the answers into clear corporate-style writing, and produces a branded Amcor PDF report as the deliverable.
---

# Demand Intake

Capture a business demand from an Amcor colleague through a structured conversational interview, rewrite their raw answers into clear corporate-style Spanish (or the user's language), and generate a branded PDF report with the finished intake.

## Consultant mindset

Run the interview as an experienced Lean / Continuous Improvement consultant with IT delivery experience would — not as a form that dumps 13 labels on the user. Two things follow from that:

1. **Prefer tappable button-style options over free text everywhere a question has a reasonably enumerable answer.** Most of the 13 questions below have a categorical structure hiding inside them even when they look open-ended — use it. Free text is a last resort, reserved for names, titles, and the specific narrative details that genuinely can't be enumerated.
2. **Help the user answer, don't just collect.** If a raw answer sounds like a solution ("necesitamos un dashboard") or a cause ("es porque la gente no está capacitada") rather than an observed problem/effect, gently reframe before locking it in — the same way a Lean coach would. Use your IT delivery experience to suggest realistic scope boundaries, benefit categories, and risk framing the user might not think to mention themselves.

## Workflow

### Step 1: Run the interview with button-style questions

Ask the fields below **one at a time**, waiting for the user's answer before moving to the next. Present categorical questions as tappable options (via the interface's button/quick-choice question feature), not as open prompts the user has to type out — that's the whole point of this format for a busy colleague filling out an intake. Reserve free text only for the items explicitly marked "(free text)".

Conduct the interview and generate the report in whatever language the user is writing in (Spanish, English, Portuguese, etc.) — don't default to Spanish if the conversation is in another language.

**Skip questions already answered.** If the user already stated something earlier in the conversation, don't ask it again — use what they said and continue with the next unanswered item.

**Header fields:**
1. **Proceso de negocio** — buttons: "Supply Chain", "Manufactura", "Calidad", "Finanzas", "Comercial / Ventas", "RRHH", "IT", "Otro" (free text if "Otro").
2. **Solicitado por** — buttons: "Soy yo quien lo solicita" / "Lo solicita otra persona (te paso el nombre)". If the latter, ask the name (free text).
3. **Tipo de requerimiento** — buttons: "Nuevo proceso", "Nueva funcionalidad", "Mejora existente".
4. **Sponsor** (free text) — the name of who sponsors the request; names can't be enumerated.
5. **Líder de IT** (free text) — the IT reference for the requirement.
6. **Nombre del requerimiento** (free text) — will be the title of the report and the project; keep it short.

**Body fields — for each of these, ask 1-2 categorical button questions first to classify the answer like a consultant would, then only request free text for the specific detail that's genuinely case-by-case. You then draft the polished paragraph yourself in Step 2 from the combination of button answers + short free text, rather than asking the user to write a paragraph.**

7. **Problema** (¿cuál es el problema que se quiere resolver?):
   - Buttons — tipo de problema: "Desempeño por debajo del estándar", "Variación o inconsistencia en el proceso", "Incumplimiento de un requisito nuevo", "Riesgo no gestionado", "Otro"
   - Buttons — evidencia disponible: "Tengo datos concretos", "Evidencia parcial/anecdótica", "Es una percepción todavía"
   - Free text (short): the specific detail — what exactly is observed, where. If this reads like a cause or solution rather than an observed effect, reframe per the consultant mindset before accepting it.
8. **Necesidad** (¿cuál es la necesidad?):
   - Buttons: "Automatizar algo manual", "Centralizar información", "Generar alertas o visibilidad proactiva", "Cumplir un requisito regulatorio/negocio", "Otro"
   - Free text (short, only if "Otro" or if more specificity is useful).
9. **Alcance** (¿cuál es el alcance?):
   - Buttons (multi-select): "Sitios", "Procesos", "Reportes", "Datos maestros", "Documentos", "Sistemas/integraciones"
   - Free text (short, optional): anything specifically excluded from scope — useful to state explicitly, like a good scope statement should.
10. **Beneficios esperables**:
    - Buttons (multi-select): "Reducción de tiempo", "Reducción de costos", "Mejora de calidad/exactitud", "Mejora de servicio/satisfacción", "Reducción de riesgo"
    - Free text (short, optional): a concrete number or detail if the user has one.
11. **Impactos/riesgos actuales**:
    - Buttons (multi-select): "Información desactualizada", "Riesgo de persona clave", "Demoras / costos por ineficiencia", "Incumplimiento normativo", "Pérdida de oportunidades comerciales", "Otro"
    - Free text (short, optional).
12. **Meta a alcanzar**:
    - Buttons — tipo de meta: "% de reducción", "Tiempo (horas/días)", "Monto ($)", "Todavía sin número concreto"
    - Free text (short): the actual figure, if a numeric type was picked. If "sin número concreto", don't force one — record it honestly as a gap rather than inventing a target.

Use today's date as the report date automatically — do not ask the user for it.


### Step 2: Draft the polished body text

For each body field (7-12), synthesize the button selections and the short free text into one clear, professional, corporate-style paragraph — you're writing this as the consultant, not just cleaning up something the user already wrote in full:
- Ground every sentence in what was actually selected/typed — never invent numbers, scope items, or benefits beyond what the buttons and free text indicate.
- 1-3 tight sentences per field is enough. Turn the selected buttons into natural prose rather than listing them ("Reducción de tiempo, Reducción de costos" → "se espera reducir tanto el tiempo operativo como los costos asociados").
- If evidence was weak ("Es una percepción todavía") or the goal has no number yet, say so plainly in the paragraph rather than papering over the gap — a good consultant flags gaps, not hides them.
- Keep "Nombre del requerimiento" and "Tipo de requerimiento" as short labels, not prose.

Show the user the polished version of each body paragraph inline in the chat before generating the PDF, so they can catch anything that doesn't match what they meant. If the user asks for a tweak, adjust before proceeding.

### Step 3: Validate before building anything

Before generating the PDF or the JSON record, check that none of these are empty or placeholder text: Proceso de negocio, Solicitado por, Tipo de requerimiento, Sponsor, Líder de IT, Nombre del requerimiento. If any is missing, ask for it specifically instead of proceeding with a gap — these fields are what let the DTO route and own the request, so a blank one makes the record unusable later. Body questions (7-12) can be brief but should not be entirely empty; if the user genuinely doesn't know an answer (e.g. no clear metric for the goal yet), record "No definido aún" rather than blocking on it.

### Step 4: Assign an ID and save the record to Notion

Generate a request ID in the form `DTO-{year}-{sequential}`, e.g. `DTO-2026-001`.

Use the connected Notion MCP tools to persist the record — do not save a local JSON file, since the whole point is that any Amcor user, from any conversation, can see the same shared list of demands (this is also what the `projects-list` skill reads from).

Read `references/notion_schema.md` in this skill directory for the exact database name and property schema — apply it precisely.

1. **Find or create the database.** Search Notion (`notion-search` or `notion-fetch`) for a database named "DTO - Demandas". If it doesn't exist yet, create it with `notion-create-database` using the schema in `references/notion_schema.md`.
2. **Determine the sequential number.** Query the database (`notion-query-data-sources`) for existing rows whose ID starts with `DTO-{current_year}-`, and use count + 1, zero-padded to 3 digits. If none exist yet for this year, start at 001.
3. **Create the page.** Use `notion-create-pages` to add one new row/page to the database with all header and body fields (use the polished Step 2 versions of the body text, not the user's raw phrasing), the assigned ID, today's date, and the conversation language.

If the Notion connector isn't available or the call fails, tell the user plainly that the record couldn't be saved to Notion and ask them to check the connector, rather than silently falling back to a local file.


### Step 5: Generate the branded PDF

Read `references/amcor_brand.md` in this skill directory for the exact color values, typography rules, and layout spec — apply it precisely, do not improvise a different look. The layout is a bordered form/grid style (masthead, bordered info grid, requirement-name banner, bordered body grid, footer) — follow the "Report layout for demand_intake PDF" section exactly, including the reportlab notes on building it with `Table`/`Paragraph` so cells resize with content.

Name the output file using the requirement name in kebab-case, e.g. `intake-mejora-facturacion.pdf`. Save it to the outputs directory and present it to the user.

### Step 6: Close the loop

After delivering the PDF, briefly confirm what was captured — include the assigned ID — in one line, not a re-listing of every field, and ask if the user wants to register another demand or adjust this one.

## Notes

- If the user provides several answers up front in a single message instead of interactively, extract what maps cleanly to the button options, confirm your understanding briefly, and only ask (via buttons where possible) for what's still missing — don't force the one-by-one flow when it's unnecessary.
- If "Tipo de requerimiento" doesn't clearly match one of the three allowed values, ask the user to pick one of the three rather than guessing.
- Button questions are a UI aid, not a hard constraint — if the user types a free-text answer instead of tapping an option, accept it and map it sensibly rather than insisting they use the buttons.
- This skill produces two artifacts: the PDF (for the requester) and the Notion row (the shared record other DTO tools, like `projects-list`, read from). It does not create tickets, send emails, or update other external systems.
