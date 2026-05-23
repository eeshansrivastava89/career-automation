---
name: interview-prep
version: 1.2.0
description: |
  Generate a company-specific interview preparation packet from the user's
  career corpus. Pulls relevant STAR stories, identifies gaps, and produces
  a concrete prep document.
license: MIT
compatibility: claude-code codex pi opencode
allowed-tools:
  - Read
  - Write
  - Edit
  - Grep
  - Glob
  - web_search
  - web_fetch
---

# Interview Prep

Generate an interview prep packet for a specific company and role.

## Prerequisites

Read `my-career/PROFILE.md`, `my-career/ACCOMPLISHMENTS.md`, and `my-career/INTERVIEW-BANK.md`. If ACCOMPLISHMENTS.md has placeholder values, tell the user to set up their corpus first.

## The Process

### 1. Understand the context

Ask: company, role, round (recruiter screen, HM, technical, case study, panel), format, any known topics. If they don't know, research the company's typical process.

### 2. Research the company

`web_search` for: common interview questions, typical process structure, what they value in candidates, recent news or strategic shifts that might come up.

### 3. Map corpus to likely questions

Cross-reference the JD with ACCOMPLISHMENTS.md:

**Strong stories** — for each JD requirement, find the best corpus story in STAR format.

**Gap areas** — flag where the user lacks direct evidence. Suggest honest reframing: "I haven't done X directly, but here's how I'd approach it based on Y."

### 4. Write the prep packet

Output to `my-career/INTERVIEW-PREP-[Company]-[Date].md`.

```markdown
# Interview Prep: [Company] — [Role]

**Date:** | **Round:** | **Format:**

---

## Company Context
- **What they do:**
- **Recent news:**
- **What they value:**
- **Interview process:**

---

## Your Positioning (2-minute intro)

> [Adapted from INTERVIEW-BANK.md, tailored closing line to this role]

---

## Likely Questions & Your Best Answers

### Behavioral / Leadership
**Q: [question]**
**Your best story:** [STAR from corpus]
**Key deliverable:** [the 1-2 sentences that must land]

### Technical / Functional
**Q: [question]**
**How to answer:** [framework from corpus]
**Watch out:** [common mistake]

### Company-Specific
**Q: "Why [Company]?"**
**Angle:** [from research]

---

## Gap Areas

| Gap | How to Address |
|-----|---------------|
| [Skill you don't have] | [Honest reframe using adjacent experience] |

---

## Your Top 5 Stories (Quick Reference)
1. **[Story]** — Tags | Use for: [question types]
2. ...

---

## Round-Specific Prep
[Customized based on round type — recruiter screen, HM, technical, case, panel]

---

## Questions to Ask Them
1. [Specific, not generic]
2. ...
```

### 5. Round-specific additions

- **Recruiter screen:** Intro, walk-me-through-resume, salary expectations (from PROFILE.md), visa talking points (from PROFILE.md)
- **HM round:** 3+ leadership stories, one failure story, 3-5 smart questions
- **Technical/SQL round:** SQL checklist from INTERVIEW-BANK.md, domain patterns
- **Case study:** Framework, company-specific likely topics, practice prompt
- **Panel/cross-functional:** Stakeholder stories, influence-without-authority stories

### 6. Anti-AI-Slop

Same rules as everywhere else. Stories should sound like something the user would actually say out loud.

### 7. Update the tracker

Move the application to `==Interviewing 🔄==` in `my-career/APPLICATIONS-TRACKER.md` with the interview date and prep doc reference.

## After the Interview

1. Add learnings to INTERVIEW-BANK.md (what questions came up, what worked, what didn't)
2. Update APPLICATIONS-TRACKER.md with the outcome
3. If rejected: brief postmortem
4. If advanced: generate prep for the next round

## Rules

1. **Stories must be real.** Only pull from the corpus. Thin stories → tell the user to flesh them out.
2. **Flag gaps honestly.** The user should know their weak spots before the interviewer finds them.
3. **Prep for the round you're getting, not every round.**
4. **Questions to ask > answers to memorize.** Every packet includes 3-5 smart questions.
5. **Practice over perfection.** Suggest the user practice their top 5 stories out loud.
6. **Read PROFILE.md for context.** Salary expectations and visa needs are in there — use them.