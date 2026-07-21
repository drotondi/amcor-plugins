---
name: practice-test
description: >
  Use this skill when a Lean Six Sigma Green Belt candidate wants to take the GB Final Exam practice test — trigger on phrases like "practice-test", "quiero rendir el examen de práctica", "tomemos el simulacro de examen", "hagamos el GB Final Exam", "practice exam", or similar requests to self-test on Green Belt material. Lets the candidate pick the exam language (Español, English, or Português) before starting, then runs a 50-question multiple-choice exam one question at a time in that language using tappable button-style answers, gives immediate right/wrong feedback with a short explanation on misses, shows a running progress bar, and produces a branded Amcor PDF at the end with every question, the answer given, the correct answer, and the final score.
---

# Practice Test (GB Final Exam)

Run a 50-question Lean Six Sigma Green Belt practice exam as an interactive, one-question-at-a-time session in chat, in the candidate's language of choice (Español, English, or Português). The candidate answers by tapping buttons (never by typing), gets instant feedback on each answer, sees a progress bar, and receives a PDF report at the end with the full answer sheet and final score.

The full question bank — with options, correct answers, and explanations — lives in `references/exam_bank.md`. Read it once at the start of the session and keep it in context for the whole exam; do not re-read it question by question. The bank's question stems are in English and its explanations in Spanish — treat that as the source of truth for meaning, not as the display language: everything shown to the candidate must be translated to the language chosen in Step 1.

## Step 1: Choose language and start the exam

Ask via buttons which language the candidate wants to take the exam in:
- **"Español"**, **"English"**, **"Português"**

Then confirm with one more button question whether they want to start now, phrased in the language just chosen:
- Start / not-now pair, e.g. **"Empezar el examen (50 preguntas)"** / **"No, ahora no"** in Spanish, **"Start the exam (50 questions)"** / **"Not now"** in English, **"Começar o exame (50 perguntas)"** / **"Agora não"** in Portuguese.

If they confirm, briefly explain the mechanics in one short message, in the chosen language (button answers, feedback per question, PDF + score at the end), and move straight to Step 2. Don't over-explain — one or two sentences is enough. Keep every remaining message of the session (questions, feedback, final score, PDF labels) in this language until the exam ends; if the candidate wants to switch language mid-exam, treat it like Step 1 again for the remaining questions but keep the score tally intact.

## Step 2: Ask questions one at a time

For **each** of the 50 questions in `references/exam_bank.md`, in order:

1. Show a plain-text progress bar as a short line before the question, e.g.:
   `Progreso: ███████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ 7/50` (translate the "Progreso" label itself, e.g. "Progress" / "Progresso").
   Build the bar proportionally (40 characters total, filled = round(40 × current/50)). This is the closest thing to a visual progress bar available in a chat turn — do not attempt to build an HTML widget per question, it would break the one-question-per-turn flow. 
2. Translate the question stem and its options into the chosen language, preserving the exact technical meaning (numbers, formulas, and DMAIC/Six Sigma terminology should use the standard term in that language, not a literal word-for-word translation where a standard term exists). Ask the question via the button-input tool (`single_select`) using the translated options as the choices.
3. Internally keep the mapping between each translated option shown and its original value/letter in the bank, so the candidate's tap can be checked against **Correcta** exactly — the translation is display-only and must never change which option is graded as correct.
4. Wait for their answer. Do not ask multiple questions in the same turn.

## Step 3: Give immediate feedback

The moment the candidate answers:

- Compare their choice (via the mapping from Step 2.3) to **Correcta** in the exam bank for that question.
- If correct: reply with a short localized "Correct" marker (**"✅ Correcto"** / **"✅ Correct"** / **"✅ Correto"**) and move straight to the next question's progress bar + question (no need to restate the explanation).
- If incorrect: reply with a short localized "Incorrect" marker (**"❌ Incorrecto"** / **"❌ Incorrect"** / **"❌ Incorreto"**), then the explanation translated into the chosen language (1-2 sentences), then state the correct answer explicitly, translated too (e.g. "La respuesta correcta era: ..." / "The correct answer was: ..." / "A resposta correta era: ..."). Then move to the next question.
- Keep feedback tight — this is a practice exam, not a lecture. One short paragraph max per question, even on misses.

Track internally, for every question: the question number, the option the candidate chose, whether it was correct, and the running score (correct/answered so far). This running tally lives only in the conversation — there's no need for external storage.

## Step 4: Final score and PDF

After question 50:

1. State the final score in chat first, in the chosen language, e.g. "X/50 correctas (Y%)" / "X/50 correct (Y%)" / "X/50 corretas (Y%)".
2. Generate a PDF exam report using the `pdf` skill (reportlab), with all labels, headers, and explanations translated into the chosen language, containing, for every question in order:
   - Question number and stem
   - The candidate's answer
   - The correct answer
   - A ✓/✗ indicator styled in **green** for correct rows and **red** for incorrect rows (use actual green/red fill or text color in the PDF — this is the one place true color is possible, unlike the chat turns)
   - For incorrect rows only, the short explanation
   - A summary block at the top or bottom with the final score and percentage
   Since this is for an Amcor audience, apply the `amcor-theme` skill for colors/typography on the report chrome (headers, title page), while keeping the per-row ✓/✗ green/red exactly as specified above (that pairing is a testing-feedback convention, not a brand color, so it overrides the theme's general palette guidance for those specific cells).
3. Save the PDF to `/mnt/user-data/outputs/` and present it with `present_files`.

## Notes

- If the candidate answers via free text instead of tapping a button, accept it and match it to the closest option rather than asking again.
- If the candidate wants to stop partway through, offer to generate the PDF with just the questions answered so far (adjust the score fraction accordingly) rather than forcing them to finish all 50.
- This skill is self-contained: it doesn't read or write charter/root-cause outputs from the other `lss-green-belt` skills.
- If the candidate wants to retake the exam, just start again from Step 1 — question order in the bank is fixed (no need to shuffle), and ask the language again rather than assuming the previous choice.
- Never show the raw English/Spanish bank text verbatim to the candidate unless their chosen language happens to match it — always pass it through the translation step described above.
