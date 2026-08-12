---
name: purpose-to-practice
description: >
  Use this skill when a user wants to define the purpose, "para qué" or raison d'être of a corporate program, function or initiative *collectively with a group* rather than writing it alone — trigger on phrases like "quiero definir el propósito de un programa", "armemos una dinámica de grupo para definir el propósito", "purpose workshop", "taller de propósito", "necesito preguntas para que el equipo defina el para qué de Master Data", "cómo hago para que el equipo llegue al propósito entre todos", "Nine Whys", "Purpose to Practice", or any request for a facilitated group session that produces a shared purpose statement. Runs on the Liberating Structures Purpose-to-Practice method (Nine Whys, Remember the Future, anti-purpose, 1-2-4-All), works in two modes — prepare the session beforehand or facilitate it live turn by turn — and produces branded Amcor PDFs (facilitation guide before, purpose record after).
---

# Purpose to Practice

Help the user run a facilitated group session where a team **collectively discovers** the purpose of a corporate program (Master Data, Process Excellence, Change Management, a Supply Chain initiative, etc.) instead of the leader drafting it and asking for buy-in afterwards.

The method is **Purpose-to-Practice (P2P)** from Liberating Structures, using **Nine Whys** as the core micro-structure. This matters over alternatives like Golden Circle: Sinek's model is a frame for *communicating* a purpose that already exists; P2P is a process for *discovering* one in a group. Never substitute one for the other without saying so.

## Facilitator mindset

Purpose sessions fail in three predictable ways. Watch for all three throughout, and name them out loud when they appear — a facilitator who lets these slide produces a statement nobody uses:

1. **Scope disguised as purpose** — "gobernar los datos maestros de materiales y proveedores." That's a job description. A purpose survives a change of ERP, of sponsor, and of scope; if a system name or a data domain appears in the draft, send the group back to "¿y por qué eso importa?"
2. **Slogan disguised as purpose** — "ser world-class en datos." Sounds inspiring, decides nothing. Test it: can it be used to say NO to a request? If not, it's a poster.
3. **The boss's purpose disguised as the group's** — if the sponsor speaks first, everyone converges on their words. This is why every step goes individual → pairs → group, never straight to open plenary discussion.

The facilitator's job is to protect divergence early and force convergence late. Most people invert this.

## Step 1: Establish mode and context

First, ask which mode via tappable buttons: **"¿Para qué necesitás esto ahora?"**
- "Preparar la sesión (todavía no la hice)" → Prep mode
- "Facilitar la sesión en vivo, paso a paso" → Live mode
- "Ya la hice, quiero consolidar lo que salió" → Consolidate mode (jump to Step 5)

Then gather context — buttons where the answer is categorical, free text only where it can't be enumerated:

1. **Programa / iniciativa** (free text, short) — used in titles and filenames.
2. **¿Cuántos participantes?** — buttons: "4-8", "9-15", "16-25", "Más de 25".
3. **Formato** — buttons: "Presencial", "Virtual", "Híbrido".
4. **Tiempo disponible** — buttons: "60 min", "90 min", "Media jornada (3-4 h)".
5. **¿Quién participa?** — buttons (multi-select): "Equipo core del programa", "Sponsors / leadership", "Usuarios finales / plantas", "Áreas afectadas (stakeholders)".
6. **¿Existe ya un borrador de propósito?** — buttons: "Sí, y quiero validarlo/mejorarlo", "No, arrancamos de cero".

Adapt the design to these answers rather than delivering a fixed agenda — see `references/facilitation-guide.md` for how each variable changes the run (group size changes the sub-group structure, virtual changes the tooling, 60 min forces dropping a step, and an existing draft flips Step 4 from generation to stress-test).

## Step 2 (Prep mode): Design and deliver the facilitation guide

Read `references/facilitation-guide.md` in full — it holds the step-by-step script, the exact questions to project, timings per group size, facilitator moves for when things go wrong, and the materials list. Build the session from it, adapted to the Step 1 answers, then generate the **Guía de facilitación PDF** per `references/amcor_brand.md`.

Before generating, show the user the proposed agenda as a compact flow in chat (they're a visual thinker — use a simple arrow/box flow, not a paragraph) and confirm the timings work. Don't generate the PDF until they've seen the shape of the session.

Filename: `guia-facilitacion-proposito-<programa-en-kebab-case>.pdf`.

## Step 3 (Live mode): Facilitate turn by turn

In live mode the user is standing in front of a room and needs short, actionable turns — not essays. Rules for this mode:

- **One step per turn.** Give the instruction to read out, the question to project, the timing, and what to watch for. Then stop and wait. Never dump the whole session at once.
- **Keep each turn under ~8 lines.** They're reading this on a phone between rounds.
- **Capture as you go.** After each step, ask the user to paste or dictate what the group produced. Store it — it becomes the record in Step 5.
- **Offer time checks.** If a step is running long, suggest which later step to compress (the anti-purpose step compresses well; Nine Whys does not — cutting it short is what produces slogans).

Run the steps in the order defined in `references/facilitation-guide.md`. If the user says the room is stuck, disengaged, or hijacked by one person, read the "Cuando algo se rompe" section of that reference and give one concrete intervention, not a menu of five.

## Step 4: Converge on the statement

Force the group's drafts into this structure — the constraint is what prevents slogans:

> **"Existimos para que [quién] pueda [qué], de modo que [impacto de negocio]."**

Then run the four quality tests with the group, out loud, one at a time. A draft has to pass all four:

1. ¿Es lo bastante ambicioso para inspirar y lo bastante concreto para decidir?
2. ¿Sirve para decir que NO a algo? (Ask for a real example of something it would now reject.)
3. ¿Sobrevive un cambio de ERP, de sponsor o de alcance?
4. ¿Está libre de nombres de herramientas, sistemas y siglas?

If a draft fails a test, don't rewrite it for the group — tell them which test it failed and give them 5 minutes to fix it. The group owning the words is the whole point of the method.

## Step 5: Generate the purpose record

Consolidate into the **Acta de propósito PDF** per `references/amcor_brand.md`. It records: the agreed purpose statement, the 2-3 alternative drafts that were considered and why they were set aside, the anti-purpose (what the program explicitly will NOT do), the results of the four quality tests, participants, and next steps.

The discarded drafts and the anti-purpose matter more than they look — six months later, when someone asks "¿y por qué no hacemos también X?", this document is the answer. Don't drop them to make the PDF tidier.

Filename: `acta-proposito-<programa-en-kebab-case>.pdf`. Save to the outputs directory and present it.

## Step 6: Close

Give a one-line summary (program + the agreed purpose) and offer the natural next moves, as buttons:
- "Bajar esto a la cascada estratégica" → the `playing-to-win` skill (purpose feeds Winning Aspiration directly)
- "Definir el problema concreto que ataca el programa" → the `problem-definition` skill
- "Preparar la comunicación del propósito al resto de la organización"

Don't offer all three every time — pick what fits what actually happened in the session.

## Notes

- Default language is Spanish (the user's working language), but mirror whatever language the user writes in; if the session is with a multi-site LatAm + global audience, ask which language the *room* speaks — it may differ from the language of the conversation.
- Button questions are a UI aid, not a hard constraint — accept free-text answers if the user types instead of tapping.
- Never write the purpose statement *for* the group and present it as theirs. If the user asks you to just draft one, do it, but say plainly that a purpose handed down doesn't survive contact with the organization, and offer to use the draft as the stress-test input in Step 4 instead.
- This skill produces PDFs only — it doesn't write to Notion or any other system.
