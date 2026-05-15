# Interview Tool — Requirements Plan

> No-backend, single-file web app. Runs locally. Invisible to the candidate. Built for the interviewer to use during the call.

---

## Core Concept

One question fills the screen at a time. The interviewer reads the question, listens, and taps signals as they hear them. No clutter. No scrolling. At the end, everything compiles into an exportable CSV.

The tool is a **decision aid during the conversation**, not a form to fill in after.

---

## Session Header (First Screen)

Before questions start, collect:

- Candidate name (text)
- Role (text or short dropdown: Senior Engineer / Staff / Principal)
- Date (auto-populated, editable)
- Interviewer name (text, optional)

This metadata appears in every CSV row.

---

## Question Screen Layout

Each screen contains exactly:

1. **Question badge** — REQUIRED or OPTIONAL (skippable)
2. **Time budget** — shown subtly (e.g. `⏱ 6–8 min`)
3. **Question text** — large, readable
4. **Drill prompts** — collapsed by default, expandable with one tap. Shows the "never accept the summary" sequence, pre-filtered to the relevant follow-ups for that question.
5. **Signal checkboxes** — 4–8 checkboxes, predefined per question. Single tap to check. No labels wrapping — short phrases only.
6. **Notes** — plain textarea, no formatting. Placeholder: `"Exact quotes go here. 'We' vs 'I' is data."`
7. **Navigation** — Previous / Skip / Next. Skip is only shown on OPTIONAL questions.

---

## Signal Checkboxes — Defined Per Question

Each question has its own checkbox set. Rough definitions:

**Opening question (48h)**
- [ ] Asked about risk first
- [ ] Mentioned observability / logs
- [ ] Asked about deploy / rollback
- [ ] Mapped critical path
- [ ] Asked about auth
- [ ] Asked questions before suggesting changes
- [ ] Mentioned domain (not just tech)

**Most uncomfortable incident**
- [ ] Named a specific incident (not generic)
- [ ] Said "I" not just "we"
- [ ] Named the first signal
- [ ] Described what went wrong
- [ ] Has a "would do differently" answer
- [ ] Emotional honesty (not just technical summary)

**Took down production**
- [ ] Has actually done it (not "almost")
- [ ] Named root cause
- [ ] Named how they found out
- [ ] Described the recovery
- [ ] Postmortem or follow-up action existed

**Hardest bug**
- [ ] Specific bug, not category of bugs
- [ ] Described debugging process, not just solution
- [ ] Named tools used
- [ ] Took longer than expected — and knows why

**Rollback**
- [ ] Has done it under pressure (not just planned)
- [ ] Knows the rollback mechanism at their company
- [ ] Describes what triggered the decision

**Monitoring**
- [ ] Names a real stack (not "we had Datadog")
- [ ] Describes what they specifically owned
- [ ] Named most important alert and why
- [ ] Has a story about something unexpected surfacing

**Technical regret**
- [ ] Names a real decision (not vague)
- [ ] Accepts personal responsibility
- [ ] Has a concrete "would do differently"

**AI workflow**
- [ ] Real example with specifics
- [ ] Names the limits or human judgment required
- [ ] Not just "autocomplete"

**General / cross-cutting signals** (always visible in a sticky sidebar or footer):
- [ ] Uses "I" consistently
- [ ] Names numbers / dates / specifics
- [ ] Asks clarifying questions
- [ ] Volunteers what they don't know

---

## End Screen

After all questions (or when interviewer taps "Finish"):

- Summary view: all questions, checked signals, and notes in one scrollable page
- Overall impression: 5-star rating or simple 3-option selector (Strong Yes / Maybe / No)
- Global notes field: free text for anything that didn't fit elsewhere
- **Export CSV** button — one click, downloads file named `[candidate-name]-[date].csv`

---

## CSV Format

One row per question. Columns:

| candidate | role | date | interviewer | question_id | question_label | required | signals_checked | signals_total | notes |
|---|---|---|---|---|---|---|---|---|---|
| Jane Doe | Senior Engineer | 2026-05-15 | Daniel | opening | 48h production access | yes | 5 | 7 | "asked about rollback before I mentioned it" |

Signal columns: comma-separated list of checked signal labels.

---

## Navigation Model

- Linear by default: question 1 → 2 → … → end
- OPTIONAL questions show a "Skip" button that records the skip in the CSV (not blank — explicitly skipped)
- Previous button always available — going back doesn't clear data
- Progress bar at top: shows position (e.g. "3 of 9")
- Keyboard navigation: → / ← for next/previous, Enter to toggle focused checkbox

---

## Data Persistence

- All state lives in `localStorage` — survives accidental tab close
- "New session" button on the end screen clears state after confirming
- No server, no accounts, no network

---

## Open Questions Before Building

These decisions will meaningfully affect scope. Resolve before coding:

1. **Single HTML file or proper project?**
   A single `.html` file is portable and zero-setup. A proper project (Vite, etc.) is easier to maintain but requires a build step. Given the use case (open on a laptop, share with a colleague), single file seems right — but confirm.

2. **Fixed question list or editable?**
   Can the interviewer add/remove/reorder questions, or is the list hardcoded from the markdown guide? Editable requires a settings screen; fixed is much simpler and still covers 90% of the use case.

3. **Styling direction?**
   - Option A: Minimal/clinical — white background, black text, no ornamentation. Fast, focused.
   - Option B: Dark mode — easier on eyes during a 90-min call.
   - Option C: Branded — Symbium colors/logo for internal use.

4. **Drill prompts: always visible or collapsed?**
   Collapsed by default keeps the screen clean. But if the interviewer is learning the technique, always-visible is a safety net. Maybe collapsed for REQUIRED questions (assumed known), always visible for first time running the tool?

5. **General signals (the "I vs we" etc.) — sticky footer or inline on every question?**
   Sticky footer keeps them visible throughout but adds permanent screen noise. Inline on every question is cleaner but requires scrolling if the question is long.
