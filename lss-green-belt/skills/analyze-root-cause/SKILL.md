---
name: analyze-root-cause
description: >
  Use this skill when a user wants to find the root cause of a problem in the Analyze phase of a DMAIC project, or needs help choosing the right statistical test to validate a cause with data — trigger on phrases like "ayudame a encontrar la causa raíz", "hagamos un 5 whys", "necesito un Ishikawa", "quiero hacer un Pareto", "qué test estadístico uso para comparar estos datos", "analyze root cause", "no sé si usar t-test o ANOVA", or similar requests for structured root-cause analysis or statistical test selection. Runs a structured interview using 5 Whys, Ishikawa, and/or Pareto with tappable button-style options wherever possible, and recommends the correct statistical test (t-test, ANOVA, chi-square, correlation, etc.) based on the data type and question, without the user having to guess.
---

# Analyze Root Cause

Guide the user through the DMAIC Analyze phase: generate and prioritize potential causes, drill down to a root cause, and recommend the right statistical test to validate it with data. This skill's deliverable is the analysis itself, delivered in chat (root cause synthesis + recommended test) — it does not produce a PDF or write to any external system.

## Consultant mindset

- Causes are hypotheses until validated with data — don't let the user (or yourself) declare a "root cause" confirmed just because it sounds plausible.
- Match the technique to where the user actually is: don't jump straight to 5 Whys if they haven't even generated a list of potential causes yet: Ishikawa comes first when the field of causes is still wide open.
- When recommending a statistical test, never guess or default to "just use a t-test" — always ground the recommendation in the actual data type and question, per `references/statistical_test_guide.md`.

## Workflow

### Step 1: Anchor the effect being analyzed

Ask, free text (short): "¿Cuál es el efecto o problema que estamos analizando?" — reuse it from earlier in the conversation (e.g. from a charter) if already stated instead of asking again.

### Step 2: Choose technique(s)

Ask via buttons (multi-select): **"Diagrama de Ishikawa (generar causas)"**, **"Pareto (priorizar con datos)"**, **"5 Whys (profundizar una causa)"**, **"No sé, ayudame a elegir"**.

If "No sé": ask one quick button question — "¿Ya tenés una lista de causas posibles o todavía no?" — "Todavía no, hay que generarlas" → recommend Ishikawa first (and Pareto after, if frequency/impact data exists); "Sí, ya tengo una o dos causas candidatas" → recommend going straight to 5 Whys on those. Read `references/rca_techniques.md` for the full guidance on when to use each technique and the recommended combination.

Run the chosen technique(s) in the order decided (Ishikawa/Pareto before 5 Whys, per the reference), looping back to offer an additional technique once one is done (e.g. "¿Ahora profundizamos con 5 Whys sobre la causa más prioritaria?").

### Step 3: Run Ishikawa (if chosen)

Read the "Ishikawa — las 6M" section in `references/rca_techniques.md`. For each of the six categories (Método, Mano de obra, Máquina, Material, Medición, Medio ambiente), ask via buttons: **"¿Hay causas potenciales en esta categoría?"** — "Sí" / "No / no aplica". If "Sí", ask free text (short list) for the causes in that category. Skip categories marked "No" without forcing content.

Close by presenting the consolidated cause list grouped by category as a simple text summary (a lightweight fishbone in words, not a PDF diagram).

### Step 4: Run Pareto (if chosen)

Ask for the categories and their frequency/impact data: free text, e.g. "tipo de defecto A: 45, tipo B: 20, tipo C: 12, otros: 8" (accept whatever format the user provides; ask for at least 3 categories to make a Pareto meaningful). Compute:
- % of each category over the total.
- Cumulative %.
- Which categories fall within the ~80% cumulative threshold — the "pocos vitales" to prioritize.

Present the ranked table and the vital-few conclusion in chat. If the result comes out flat (no clear vital few), say so per the reference and suggest re-stratifying the data or going deeper with Ishikawa instead of forcing a conclusion.

### Step 5: Run 5 Whys (if chosen)

Read the "5 Whys — reglas prácticas" section in `references/rca_techniques.md`. Take the prioritized cause (from Ishikawa/Pareto, or whatever the user names) as the starting effect. Ask, free text: **"¿Por qué pasa esto?"** — repeat using the previous answer as the new effect, up to 5 rounds.

After each answer, ask via buttons: **"¿Llegamos a algo accionable y verificable, o seguimos profundizando?"** — "Es accionable, paremos acá" / "Seguir profundizando" / "No estoy seguro, es una suposición sin base". If the last option is picked, don't keep drilling on a guess — flag that this branch needs data before continuing, and either ask for that data now (if the user has it) or note it as an open validation item.

### Step 6: Recommend the statistical test to validate the root cause

Ask, via buttons, what the user wants to test: **"Comparar el promedio entre 2 grupos"**, **"Comparar el promedio entre 3+ grupos"**, **"Ver si dos variables categóricas están relacionadas"**, **"Ver la relación entre dos variables numéricas"**, **"Ver si la variabilidad difiere entre grupos"**, **"No estoy seguro"**.

Then, depending on the answer, ask the follow-up questions needed per `references/statistical_test_guide.md` (Paso 1 y 2) — e.g. for a 2-group comparison: "¿Los datos son pareados (mismos elementos antes/después) o independientes?" and "¿Los datos son aproximadamente normales?" (offer the buttons: "Sí, parecen normales", "No, están sesgados o tienen outliers", "No estoy seguro cómo verlo" — if unsure, briefly explain the histogram/normal-plot check from the reference before asking again).

Read the full decision tree in `references/statistical_test_guide.md` and recommend the specific test by name (e.g. "test t de 2 muestras independientes", "ANOVA de un factor + Tukey", "Chi-cuadrado de independencia", "Mann-Whitney U"), explaining in one sentence why that test fits their data — don't just name it without the reason.

If the user comes back with a result (p-value), interpret it per the "Interpretación del resultado" section — statistical significance and practical relevance are not the same thing, say so explicitly.

### Step 7: Synthesize

Close with a short synthesis in chat:
- **Causa raíz identificada** (or candidate, if not yet data-validated) — one sentence.
- **Evidencia que la respalda** — what from Ishikawa/Pareto/5 Whys supports it.
- **Test estadístico recomendado** (if applicable) and what result would confirm or reject it.
- **Próximo paso** — validate with data if not done yet, or move to Improve if already validated.

## Notes

- Don't force all three techniques every time — a user who just wants test-selection help (Step 6 only) shouldn't be walked through Ishikawa first; ask Step 1 and jump to Step 6 if that's clearly all they need.
- Button questions are a UI aid — accept free-text answers if the user types instead of tapping.
- This skill is independent of `define-charter` and `gb-coach` — it doesn't read their outputs automatically, but the effect/problem from a charter, or feedback from a `gb-coach` Analyze review, can be pasted in as context.
