# Senior Engineer Interview — Early-Stage Startup

> For companies with momentum but small teams (~3 people). You're not hiring for potential. You're hiring for someone who can own production tomorrow.

---

## The Opening Question (Never Skip This)

**⏱ 8–10 min — REQUIRED**

> "Imagine you get production access to our system tomorrow. What do you try to understand in the first 48 hours?"

**What a real operator says:**
- Asks about risk before suggesting changes
- Mentions observability, logs, monitoring
- Asks about deploy process and rollback
- Maps the critical path and auth flows
- Asks about queues, async jobs, failure modes
- Wants to understand the domain, not just the stack

**Red flag:** jumps to "I'd refactor X" or asks about tech stack before asking about risk.

---

## The Core Technique: Never Accept the Summary

Every significant answer gets drilled with this sequence:

```
"Tell me exactly how that happened."
→ "What was the problem before?"
→ "How did you find out?"
→ "What was the first signal?"
→ "What did you do first?"
→ "What went wrong?"
→ "What would you do differently today?"
```

The summary is rehearsed. The drill is real.

---

## High-Signal Questions

### Production Proximity

- **⏱ 6–8 min — REQUIRED** "Tell me about the most uncomfortable incident you've been through."
- **⏱ 5–7 min — REQUIRED** "Have you ever taken down production? Walk me through it."
- **⏱ 4–6 min — REQUIRED** "What's the hardest bug you've ever debugged?"
- **⏱ 4–5 min — skip if rollback came up in incident** "Have you ever had to do an emergency rollback? What triggered it?"
- **⏱ 2–3 min — skip if on-call came up naturally** "What does your on-call setup look like at your current job?"

### Observability & Monitoring

- **⏱ 5–7 min — skip if covered in incident question** "What were you monitoring? Walk me through the stack."
- **⏱ 2–3 min — skip if irrelevant to role** "What was the most important alert you had?"
- **⏱ 4–6 min — REQUIRED if observability is a gap on our team** "Which incident did monitoring help you catch — and what did you find that you didn't expect?"

### Judgment & Trade-offs

- **⏱ 5–6 min — REQUIRED** "Tell me about a technical decision you made that you later regretted."
- **⏱ 3–5 min — skip if personality is already clear** "When was the last time you pushed back on a feature request for technical reasons?"
- **⏱ 3–5 min — skip if irrelevant** "Have you ever had to choose between shipping fast and doing it right? What happened?"

### AI Workflow

**⏱ 4–6 min — skip if role is not expected to work autonomously with AI**

- "Give me a real example where AI dramatically changed your velocity."
  - Follow up: "Which parts still needed human judgment?"

**Strong answers include:** debugging, test generation, semantic search, refactoring, onboarding, characterization tests, scripting, automation — **plus** validation, review, knowing the limits.

**Weak answers:** "I use Copilot for autocomplete."

---

## Domain Coverage Checklist

Force a concrete example for each area you care about:

- [ ] Incidents & postmortems
- [ ] Deploy process (CI/CD, feature flags, rollback)
- [ ] Debugging under pressure
- [ ] Monitoring & alerting
- [ ] Recovery from downtime
- [ ] Security decisions
- [ ] Trade-offs made under time pressure

---

## What You're Listening For

| Signal | Meaning |
|---|---|
| Asks questions before proposing solutions | Operator mindset |
| Talks about risk unprompted | Production-aware |
| Names specific tools and numbers | Real experience |
| Mentions what went wrong | Honest, not just curated wins |
| Knows what they don't know | Self-aware |
| Vague about how things worked | Watching from a distance, not doing |
| Only talks about greenfield work | May not have owned anything messy |
| No incidents to speak of | Protected from production or exaggerating scope |

---

## Disqualifying Patterns

- Can't name a single incident with specifics
- Answers every question with "we" but can't say what *they* personally did
- Has never done a deploy or rollback themselves
- Suggests architectural changes before understanding the system
- No opinion on monitoring or failure modes

---

## Notes

Use this file as a running doc during the interview. Write down exact quotes — especially when someone uses "we" instead of "I." That delta is data.
