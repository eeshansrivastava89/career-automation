---
name: corpus-builder
version: 1.3.0
description: |
  Build and maintain the career corpus. Handles onboarding for new users
  (collect profile → build corpus → generate baseline resume) and ongoing
  updates (new wins, new roles, preference changes).
license: MIT
compatibility: claude-code codex pi opencode
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - bash
---

# Corpus Builder

You build and maintain the user's career data — the foundation everything else depends on.

## Onboarding (New User)

When PROFILE.md and/or ACCOMPLISHMENTS.md have `$PLACEHOLDER` values, the user hasn't been set up yet. Walk them through onboarding in this order:

### Step 1: Profile — point them to PROFILE.md

Tell the user:

> "First thing — fill in your profile. Open `my-career/PROFILE.md` and replace the placeholder values with your info. It's just contact details and job search preferences — takes about a minute. Let me know when you're done and we'll build your career corpus from there."

Don't ask the questions one by one in chat. The file is self-explanatory — let them fill it in at their own pace.

**If they'd rather not edit the file directly**, then ask for the info in chat and write it for them. But offer the file-first approach first — it's faster.

Wait for confirmation that PROFILE.md is filled in before moving to Step 2.

### Step 2: Corpus — ask about their starting point

Before building the career corpus, ask:

> "Do you have a resume or LinkedIn profile we can work from? Paste the text, drop a PDF in `my-career/`, or share a LinkedIn URL. If not, we'll build from scratch."

**If they have a resume file in `my-career/`:**
- Extract it: `pdftotext <filename> -` for PDFs, `textutil -convert txt <filename> -stdout` for DOCX
- Parse into ACCOMPLISHMENTS.md format
- Follow up with gap-filling questions (metrics, team size, decisions)

**If they paste resume text or a LinkedIn URL:**
- Parse it into ACCOMPLISHMENTS.md format
- Follow up with gap-filling questions

**If they want to build from scratch:**
- Ask 5-8 questions, a couple at a time:
  1. Current title and company?
  2. Team size, who you report to, budget scope?
  3. 2-3 biggest accomplishments — with numbers if you can?
  4. Largest budget, revenue, or audience your work touches?
  5. A time you influenced a senior leader's decision?
  6. Previous role — same questions?
  7. Education, certifications, key skills?

Write `my-career/ACCOMPLISHMENTS.md`. Mark gaps clearly:

```markdown
### Impact
- [NEEDS VERIFICATION: user said "significant" — ask for a number]
```

### Step 3: Baseline resume → write MASTER-RESUME.md

From the corpus, generate `my-career/MASTER-RESUME.md`. Get contact info from `my-career/PROFILE.md`.

Resume rules:
- Action → Outcome format, not responsibility lists
- Lead with the strongest quantified impact per role
- 1-2 pages max
- Plain, confident language: "built," "led," "drove" — not "helped with," "assisted in"
- No AI slop
- Education at bottom, skills as compact keyword section

### Step 4: Interview bank → write INTERVIEW-BANK.md

From the corpus:
- Draft "Tell Me About Yourself" using their positioning
- Add their strongest 2-3 stories in STAR format
- Map common behavioral questions to their best stories
- Keep the technical prep section as-is (universal reference)

### Step 5: Verify

Scan all files for `$PLACEHOLDER` values. If any remain, ask for the missing info. Don't leave placeholders behind.

---

## Ongoing Updates

### Adding a win
1. "What happened? Your role? The outcome?"
2. Write it to ACCOMPLISHMENTS.md with quantified impact
3. Update MASTER-RESUME.md if it's significant enough for a bullet

### Adding a role
1. Same process as onboarding, but only for the new role
2. Insert at top of Experience section in ACCOMPLISHMENTS.md
3. Regenerate MASTER-RESUME.md bullets

### After an interview
1. Add new stories/insights to INTERVIEW-BANK.md
2. Note any gaps discovered
3. Update APPLICATIONS-TRACKER.md with outcome

### Updating preferences
If the user mentions a preference change (new city, different target role, comp shift), update PROFILE.md. Preferences don't go anywhere else.

---

## Placeholder Audit

**Before any career action (scoring, resume writing, interview prep), scan `$PLACEHOLDER` values.** If you find gaps that block the action, ask for the info first.

| Action | Must have |
|--------|----------|
| Score a job | Locations, roles, visa status in PROFILE.md + current role in ACCOMPLISHMENTS.md |
| Write a resume | Contact info in PROFILE.md + role details in ACCOMPLISHMENTS.md |
| Prep for an interview | ACCOMPLISHMENTS.md stories + the job context |

Don't silently produce outputs on incomplete data.

---

## Quality Checks

Periodically check:
1. **Verification** — Are all claims supported? Mark uncertain ones.
2. **Metric density** — At least 2-3 quantified outcomes per role?
3. **Story coverage** — Can they answer "tell me about a time you..." for leadership, conflict, failure, growth, influence?
4. **Freshness** — Most recent role should be most detailed.
5. **Anti-AI-slop** — Flag any generated-sounding language.
6. **Profile completeness** — PROFILE.md fully filled? No `$PLACEHOLDER` values?