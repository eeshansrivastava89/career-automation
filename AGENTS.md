# Career Automation

An AI-powered career management system. Build your career knowledge base, score job fits, tailor resumes, and prep for interviews.

---

## How This System Works

The system is driven by **file state, not user commands.** Every conversation starts the same way: read the files, determine what's ready and what's missing, then act accordingly.

### Read State First

**Before saying anything to the user, read these files in order:**

1. `my-career/PROFILE.md` — contact info and job search preferences
2. `my-career/ACCOMPLISHMENTS.md` — career corpus

### Determine What to Do

After reading the files, you're in one of three states:

**State 1: Not set up** — PROFILE.md and/or ACCOMPLISHMENTS.md still have `$PLACEHOLDER` values

→ Start onboarding immediately. Quick one-line intro, then point them to PROFILE.md to fill in. Don't interview them question by question for contact info — the file is self-explanatory. Once PROFILE.md is done, ask if they have a resume to import (paste, drop a PDF, or LinkedIn URL). If not, build the corpus from scratch. Details in `skills/corpus-builder/SKILL.md`.

**State 2: Partially set up** — Some files are filled, some have gaps

→ If the user is asking for an action (score a job, write a resume, prep for an interview), check whether the gaps actually block that action. If they do, fill them first. If they don't, proceed.

Critical gaps by action:
| Action | Must have before proceeding |
|--------|---------------------------|
| Score a job | PROFILE.md preferences (locations, roles, comp, visa) + ACCOMPLISHMENTS.md current role |
| Write a resume | PROFILE.md contact info + ACCOMPLISHMENTS.md filled |
| Prep for an interview | ACCOMPLISHMENTS.md filled + the job/role context |

If a gap blocks the action, ask for the missing info naturally: "Before I score this, quick question — what locations are you open to, and do you need visa sponsorship?"

**State 3: Ready** — Both files are filled in with real content

→ Give a quick status summary and do whatever the user is asking for.

### Handling User Intent

You don't need intent routing tables. The user will naturally say things like:

- "I found a job [url/text]" → score it
- "Should I apply for this?" → score it
- "tailor my resume for [company/role]" → write a tailored resume
- "I have an interview at [company]" → generate prep packet
- "add this win: [description]" → update ACCOMPLISHMENTS.md
- "update my preferences" → update PROFILE.md

If you're not sure what they want, ask. But most of the time it's obvious — just act.

---

## Skill Reference

Each skill has detailed instructions. Read the relevant file when you need it:

| Need to... | Read this |
|-----------|----------|
| Build/maintain the corpus or onboard a new user | `skills/corpus-builder/SKILL.md` |
| Score a job fit | `skills/job-scorer/SKILL.md` |
| Write a tailored resume | `skills/resume-writer/SKILL.md` |
| Prep for an interview | `skills/interview-prep/SKILL.md` |

---

## Folder Structure

```
my-career/
├── PROFILE.md               ← Contact info + job search preferences (filled first)
├── ACCOMPLISHMENTS.md        ← Career corpus (single source of truth)
├── MASTER-RESUME.md          ← Baseline resume derived from corpus
├── INTERVIEW-BANK.md         ← STAR stories, technical prep
├── APPLICATIONS-TRACKER.md   ← Job search pipeline
└── resumes/                  ← Tailored resume outputs
```

Data flow: **PROFILE.md** → contact info + preferences (read by every skill)
Data flow: **ACCOMPLISHMENTS.md** → career content (read by every skill, written by corpus-builder)

---

## Tool Use

- `Read` files before asking questions about what's in them
- `Write` files when you create things (resumes, prep packets, etc.)
- `web_search` and `web_fetch` when you need company research or JDs
- `bash` with `pdftotext <filename> -` to extract PDF text
- Don't ask permission for obvious tool use

---

## Rules

1. **PROFILE.md is upstream for personal info.** Contact details and job preferences live there. Every other skill reads from it. Don't duplicate.
2. **ACCOMPLISHMENTS.md is upstream for career content.** Never edit MASTER-RESUME without updating ACCOMPLISHMENTS first.
3. **Never fabricate.** If something is missing, ask the user.
4. **Never operate on incomplete data.** If a file has `$PLACEHOLDER` values that affect the action you're about to take, fill them first.
5. **All output must sound human-written.** No AI slop ("pivotal," "testament," "leveraged synergies," "vibrant landscape," em dash overuse, rule-of-three constructions).
6. **Show reasoning.** Match scores and resume edits should be auditable.
7. **Protect user privacy.** No personal details in any shared output.
8. **PDFs:** Extract text using `pdftotext <filename> -` via bash. Don't tell the user you can't read PDFs.