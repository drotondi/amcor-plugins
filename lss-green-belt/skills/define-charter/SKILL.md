---
name: define-charter
description: >
  Use this skill when a user wants to build a Lean Six Sigma Project Charter for the Define phase of a DMAIC project — trigger on phrases like "armá el charter de mi proyecto", "necesito un project charter", "define charter", "quiero documentar el alcance y el business case de mi proyecto Six Sigma", or similar requests to formalize a project's problem, scope, VOC/CTQs, SIPOC, team, and business case. Runs a structured interview using tappable button-style options wherever possible, drafts the polished charter content, and produces a branded Amcor PDF as the deliverable.
---

# Define Charter

Guide the user through building a Lean Six Sigma Project Charter — the standard Define-phase deliverable: problem statement, scope, VOC/CTQs, SIPOC, team, and business case. Run the interview like an experienced Master Black Belt would when coaching a Green Belt candidate through their first charter, then generate a branded Amcor PDF as the deliverable.

## Consultant mindset

- Prefer tappable button-style options over free text everywhere the answer is categorical — free text is reserved for names, specific metrics, and narrative details that can't be enumerated.
- Don't just transcribe what the user says — if a "problem" sounds like a solution or a cause rather than an observed effect, gently redirect before locking it in (same discipline as a real Define-phase review).
- If the user hasn't thought about a section yet (e.g. no VOC captured), don't force a fabricated answer — help them think it through with a couple of guiding questions, or record it honestly as "pendiente de validar" rather than inventing content.

## Workflow

### Step 1: Header fields (buttons where possible)

Ask one at a time; skip anything already stated earlier in the conversation:
1. **Nombre del proyecto** (free text, short) — used as PDF title and filename.
2. **Green Belt candidato** (free text) — name of who's running the project.
3. **Sponsor** (free text).
4. **Champion / Mentor (MBB)** (free text).
5. **Área o proceso** — buttons: "Supply Chain", "Manufactura", "Calidad", "Finanzas", "Comercial / Ventas", "RRHH", "IT", "Otro" (free text if "Otro").
6. **Fecha de inicio** — buttons: "Hoy", "Ya arrancó hace tiempo (decime la fecha)", use today's date automatically for "Hoy"; free text date otherwise.
7. **Fecha objetivo de cierre** — buttons: "1 mes", "3 meses", "6 meses", "Otra (decime la fecha)" — convert relative options to an actual date from the start date.

### Step 2: Problem statement (evidence-based, cause-free, solution-free)

Ask, one at a time, as buttons unless marked free text:
1. **Tipo de problema**: "Desempeño por debajo del estándar", "Variación o inconsistencia en el proceso", "Incumplimiento de un requisito nuevo", "Riesgo no gestionado", "Otro".
2. **Evidencia disponible**: "Tengo datos concretos", "Evidencia parcial/anecdótica", "Es una percepción todavía".
3. **¿Dónde y desde cuándo?** (free text, short).
4. **Magnitud del impacto**: "Bajo", "Medio", "Alto", "Crítico".

Draft a single problem-statement paragraph from these answers (evidence-based, no cause, no solution). If the raw input sounded like a cause or solution, leave it out of the statement and mention it to the user as something to explore later in Analyze, not here.

### Step 3: Goal statement

1. **Métrica a mejorar** (free text, short) — e.g. "% de scrap", "tiempo de ciclo", "NPS".
2. **Dirección deseada** — buttons: "Reducir", "Aumentar", "Eliminar", "Estabilizar (reducir variación)".
3. **Línea base actual** (free text) — the current value, or "Sin dato aún" if unknown.
4. **Meta objetivo** (free text) — the target value, or "Sin número aún" if the user genuinely doesn't have one — don't invent it.
5. **Plazo** — reuse the target close date from Step 1 unless the user wants a different milestone for this specific metric.

Draft one goal-statement sentence, e.g. "Reducir el % de scrap de la línea 3 de 8% a 3% para [fecha]."

### Step 4: Business case

1. **Tipo de beneficio** — buttons (multi-select): "Reducción de costos", "Reducción de tiempo", "Mejora de calidad", "Mejora de servicio/satisfacción", "Reducción de riesgo/cumplimiento".
2. **¿Hay un número estimado?** — buttons: "Sí, tengo una cifra", "No, todavía no lo cuantificamos". If yes, ask the figure (free text, short, e.g. "USD 45,000/año" or "20 horas/mes").
3. **Costo de no hacer nada** (free text, short, optional) — what happens if this problem isn't addressed; helps justify urgency.

Draft one business-case paragraph combining the benefit type(s), the figure if given, and the cost of inaction if given.

### Step 5: VOC and CTQs

Explain briefly: "Vamos a traducir lo que el cliente necesita en algo medible (CTQ)." Then, for 2-4 rounds (ask "¿Agregamos otra voz de cliente?" via buttons Sí/No after each):
1. **Cliente** — buttons: "Cliente externo", "Cliente interno / otra área", "Regulador / cumplimiento", "Otro".
2. **Necesidad expresada (VOC)** (free text, short) — what the customer actually said or would say.
3. **CTQ derivado** — help the user translate the VOC into a measurable requirement (a metric + spec/threshold). If they're unsure, suggest one based on the VOC and confirm with them rather than asking them to invent it alone.

### Step 6: SIPOC

Walk through each column, one at a time:
1. **Process** (free text) — ask for the 4-7 high-level steps of the process in scope, in order. This anchors the rest.
2. **Suppliers** (free text, short list) — who provides inputs to this process.
3. **Inputs** (free text, short list) — what feeds into the process (materials, data, requests).
4. **Outputs** (free text, short list) — what the process produces.
5. **Customers** (free text, short list) — who receives the outputs; cross-check this is consistent with Step 5's VOC customers.

### Step 7: Scope

1. **Incluye** — buttons (multi-select): "Sitios específicos", "Un proceso/línea específica", "Un producto/familia específica", "Un turno/horario específico", "Otro" (free text detail for whichever is picked).
2. **No incluye** (free text, short, optional but encouraged) — anything explicitly excluded; a good charter states this rather than leaving it implicit.

### Step 8: Team

For each member (repeat until the user says "No hay más miembros"):
1. **Nombre** (free text).
2. **Rol** — buttons: "Sponsor", "Champion/MBB", "Green Belt (líder)", "Miembro del equipo", "Subject Matter Expert".
3. **Dedicación** — buttons: "Full-time durante el proyecto", "Part-time regular", "Consulta puntual".

(Sponsor, Champion/MBB, and Green Belt from Step 1 can be added automatically as the first three rows — just confirm dedication for each rather than re-asking name and role.)

### Step 9: Validate before building

Check that Nombre del proyecto, Green Belt candidato, Sponsor, the problem statement, and the goal statement are not empty or placeholder. If any is missing, ask for it specifically. Sections that are legitimately "pendiente" (e.g. no CTQ defined yet) can be recorded as such — don't block the whole charter on one open item, but flag it clearly in the PDF rather than hiding the gap.

### Step 10: Generate the branded PDF

Read `references/amcor_brand.md` in this skill directory for the exact colors, typography, and layout — apply it precisely, including the SIPOC and VOC/CTQ table structure described there.

Name the file using the project name in kebab-case, e.g. `charter-reduccion-scrap-linea-3.pdf`. Save it to the outputs directory and present it to the user.

### Step 11: Close the loop

After delivering the PDF, give a one-line summary (project name, problem in a phrase, goal) — not a re-listing of every field. Ask if the user wants to adjust anything or move on, e.g. to a `gb-coach` review of this Define phase.

## Notes

- If the user provides several answers up front in one message, extract what maps cleanly, confirm briefly, and only ask for what's missing.
- Button questions are a UI aid, not a hard constraint — accept free-text answers if the user types instead of tapping.
- This skill produces only the PDF — it doesn't write to Notion or any other system, and it's independent of `gb-coach` and `analyze-root-cause`, though its output is a natural input to hand to `gb-coach` for a Define tollgate review.
