---
name: resume-writer
version: 1.2.0
description: |
  Generate a tailored resume from the user's career corpus for a specific role.
  Truthful emphasis, not keyword stuffing. Anti-AI-slop built in.
license: MIT
compatibility: claude-code codex pi opencode
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
---

# Resume Writer

Generate a tailored resume for a specific job application. Output is clean markdown the user can paste into Google Docs or any editor.

## Prerequisites

Read `my-career/PROFILE.md`, `my-career/ACCOMPLISHMENTS.md`, and `my-career/MASTER-RESUME.md` before starting. Contact info comes from PROFILE.md. If PROFILE.md contact info has placeholders, ask for it before writing.

## The Process

### 1. Read source material

Read PROFILE.md (contact header), ACCOMPLISHMENTS.md (career content), MASTER-RESUME.md (baseline), and the target JD or match report.

### 2. Identify what matters

From the JD: top 3 skills, seniority level, scope signals, domain language.

### 3. Reorder and reframe — don't invent

**You CAN:**
- Reorder bullets so the most relevant impact is first
- Reframe accomplishments using the role's language
- Emphasize different metrics depending on what the role values
- Expand a one-line corpus entry into 2 bullets if directly relevant
- Condense less-relevant bullets (keep a mention for breadth)

**You CANNOT:**
- Add skills the user doesn't have
- Inflate titles or team sizes
- Invent metrics or outcomes
- Add preferred qualifications the user doesn't possess (flag these as gaps instead)

### 4. Write the tailored resume

Output to `my-career/resumes/RESUME-[Company]-[YYYY-MM-DD].md`. Create the `resumes/` folder if needed.

**Structure:**
```markdown
# [User Name]
[Email] | [Phone] | [Location] | [LinkedIn] | [GitHub] | [Portfolio]

---

## Summary
[2-3 lines. Level, domain, highest-impact signal. No adjective soup.]

---

## Experience
### [Company] — [Location]
**[Title]** | [Start] – Present
- [Bullet 1: strongest quantified impact relevant to target role]
- [Bullet 2: next strongest]
- [Bullet 3: scope/team/method signal]
...

---

## Education
**[Degree]** | [School], [Location] | [Dates]

---

## Skills
- **[Category]**: skill, skill, skill
```

Contact info comes from PROFILE.md. Don't hardcode it.

### 5. Document what changed

Add tailoring notes at the end:

```markdown
<!-- TAILORING NOTES (remove before submitting)
Job: [Company] — [Title]
Date: [Today]

Changes from MASTER-RESUME:
1. [What changed and why]
2. ...

Gaps:
- [JD asks for X, user doesn't have it]
-->
```

### 6. Anti-AI-Slop Pass

Scan for and eliminate:
- **Banned words:** pivotal, testament, vibrant landscape, leverage (as verb), synergy, utilize, foster, spearheaded, catalyze, orchestrated, championed, streamlined, empower, "drove cross-functional alignment"
- **Em dash overuse:** max 1-2 per resume
- **Rule of three:** "built, scaled, and optimized..." — break the pattern
- **Boldface abuse:** not every metric needs bold

**Litmus test:** Read every bullet out loud. If it sounds like an AI wrote it, rewrite it.

### 7. Update the tracker

Add or update the application in `my-career/APPLICATIONS-TRACKER.md` with `==Applied ✅==`.

## Rules

1. **Truth > match.** A lower score with an honest resume beats faked alignment.
2. **Every change is traceable.** Tailoring notes must exist in every output.
3. **Corpus is upstream.** If a detail needs adding, add it to ACCOMPLISHMENTS.md first.
4. **Profile is upstream for contact info.** Get name, email, phone, LinkedIn from PROFILE.md.
5. **One page for IC roles, 1.5-2 pages for manager/director.**
6. **Numbers first.** "$50M," "10-person team," "100+ experiments."