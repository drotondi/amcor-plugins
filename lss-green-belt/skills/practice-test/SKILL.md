---
name: practice-test
description: >
  Use this skill when a Lean Six Sigma Green Belt candidate wants to take the GB Final Exam practice test — trigger on phrases like "practice-test", "quiero rendir el examen de práctica", "tomemos el simulacro de examen", "hagamos el GB Final Exam", "practice exam", or similar requests to self-test on Green Belt material. Runs a 50-question multiple-choice exam one question at a time using tappable button-style answers, gives immediate right/wrong feedback with a short explanation on misses, shows a running progress bar, and produces a branded Amcor PDF at the end with every question, the answer given, the correct answer, and the final score.
---

# Practice Test (GB Final Exam)

Run a 50-question Lean Six Sigma Green Belt practice exam as an interactive, one-question-at-a-time session in chat. The candidate answers by tapping buttons (never by typing), gets instant feedback on each answer, sees a progress bar, and receives a PDF report at the end with the full answer sheet and final score.

The full question bank — with options, correct answers, and explanations — lives in `references/exam_bank.md`. Read it once at the start of the session and keep it in context for the whole exam; do not re-read it question by question.

## Step 1: Start the exam

Confirm with one button question whether the candidate wants to start now:
- **"Empezar el examen (50 preguntas)"**, **"No, ahora no"**

If they confirm, briefly explain the mechanics in one short message (button answers, feedback per question, PDF + score at the end) and move straight to Step 2. Don't over-explain — one or two sentences is enough.

## Step 2: Ask questions one at a time

For **each** of the 50 questions in `references/exam_bank.md`, in order:

1. Show a plain-text progress bar as a short line before the question, e.g.:
   `Progreso: ███████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ 7/50`
   Build the bar proportionally (40 characters total, filled = round(40 × current/50)). This is the closest thing to a visual progress bar available in a chat turn — do not attempt to build an HTML widget per question, it would break the one-question-per-turn flow.
2. Ask the question via the button-input tool, using the question's exact options as the choices (`single_select`). Keep the question stem verbatim from the bank (English, as in the original exam) so it matches what the candidate is studying from.
3. Wait for their answer. Do not ask multiple questions in the same turn.

## Step 3: Give immediate feedback

The moment the candidate answers:

- Compare their choice to **Correcta** in the exam bank for that question.
- If correct: reply with **"✅ Correcto"** and move straight to the next question's progress bar + question (no need to restate the explanation).
- If incorrect: reply with **"❌ Incorrecto"**, then the explanation from the bank (1-2 sentences), then state the correct answer explicitly, e.g. "La respuesta correcta era: ...". Then move to the next question.
- Keep feedback tight — this is a practice exam, not a lecture. One short paragraph max per question, even on misses.

Track internally, for every question: the question number, the option the candidate chose, whether it was correct, and the running score (correct/answered so far). This running tally lives only in the conversation — there's no need for external storage.

## Step 4: Final score and PDF

After question 50:

1. State the final score in chat first: "X/50 correctas (Y%)".
2. Generate a PDF exam report using the `pdf` skill (reportlab) containing, for every question in order:
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
- If the candidate wants to retake the exam, just start again from Step 1 — question order in the bank is fixed (no need to shuffle).
