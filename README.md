# Career Automation

An AI-powered career management system. Build your career knowledge base, score job fits, tailor resumes, and prep for interviews — all from one folder.

**For non-technical users.** You need an AI agent (Claude Code, Codex, Pi, OpenCode, etc.) and this folder. No terminal needed. No code to write. No LaTeX.

---

## What This Does

Most AI resume tools are single-shot: you paste a JD, they spit out a generic resume. This system is **corpus-driven**. You build a career knowledge base once, and every output (resume, match score, interview prep) derives from it. The more you add, the smarter the agent gets about you.

## How It Works

The system is driven by **what's in your files**, not by magic commands.

1. **First time?** The agent sees that your `my-career/` files are empty. It walks you through setting up your profile and career corpus. This takes about 15 minutes.
2. **After that?** The agent reads your files and does whatever you're asking for — score a job, write a resume, prep for an interview. If something's missing that affects the action, it asks you first.

No special commands to remember. Just talk to the agent naturally.

---

## Quick Start

1. **Download this repo** (clone it, or download the ZIP)
2. **Open your AI agent** in this folder (Claude Code, Codex, Pi, OpenCode, etc.)
3. **Say anything** — the agent reads `AGENTS.md`, sees your files are empty, and starts onboarding you
4. Answer questions about your career. The agent builds your corpus. Done.

No install command. No terminal. No setup script.

---

## Match Scoring

Every job is scored across 5 dimensions (0-20 each, 0-100 total):

| Dimension | What It Measures |
|-----------|------------------|
| Skill Overlap | How directly your skills match the JD's requirements |
| Seniority Fit | Whether your level matches the role's level |
| Domain Relevance | How relevant your industry experience is |
| Team/Scope Fit | Whether your leadership experience matches the scope |
| Edit Effort | How much resume rework needed (inverted — less is better) |

Plus a **preference fit** check: does the job's location, comp, and visa status match what you're looking for?

| Score | Recommendation |
|-------|---------------|
| 85-100 | **Apply** — strong fit |
| 70-84 | **Apply if interested** — good fit, some gaps |
| 55-69 | **Stretch** — notable gaps, apply for practice |
| 0-54 | **Skip** — poor fit, move on |

Every score comes with reasoning you can audit.

---

## What Makes This Different

**1. Corpus-driven, not prompt-driven.** Other tools generate a resume from whatever you paste in chat. This system builds from a maintained knowledge base that grows over time.

**2. Match scoring with rationale.** Every dimension has a score and notes explaining it. You can challenge any score.

**3. Company research built in.** The agent researches every company before recommending you apply. Layoffs, bad reviews, financial instability — it surfaces the risks.

**4. Anti-AI-slop.** All output is scanned for AI-generated language patterns. No "pivotal," "testament," "leveraged synergies." Writes like a concise professional.

**5. Truthful emphasis.** The agent will not add skills you don't have, inflate titles, or keyword-stuff. If a gap exists, it tells you.

**6. Interview prep, not just resumes.** Score → apply → tailor → prep. One workflow.

---

## Folder Structure

```
career-automation/
├── AGENTS.md                ← Agent reads this first. Entry point.
├── skills/                  ← System instructions (don't edit)
│   ├── corpus-builder/SKILL.md   ← Onboarding + corpus management
│   ├── job-scorer/SKILL.md        ← Job fit evaluation
│   ├── resume-writer/SKILL.md    ← Tailored resume generation
│   └── interview-prep/SKILL.md   ← Interview preparation
├── my-career/               ← Your career files (agent creates these)
│   ├── PROFILE.md                 ← Contact info + job search preferences
│   ├── ACCOMPLISHMENTS.md         ← Your career corpus (source of truth)
│   ├── MASTER-RESUME.md           ← Baseline resume
│   ├── INTERVIEW-BANK.md          ← Stories and technical prep
│   ├── APPLICATIONS-TRACKER.md    ← Job search pipeline
│   └── resumes/                   ← Tailored resume outputs
├── tests/                   ← Example end-to-end flow
├── README.md
└── LICENSE
```

**You only need to care about `my-career/`.** Everything else is system files.

---

## Requirements

- An AI agent that supports custom instructions or project prompts (Claude Code, Codex, Pi, OpenCode, etc.)
- A text editor (Obsidian recommended, any markdown editor works)
- No code, no terminal, no LaTeX, no scripts

---

## License

MIT — use it, modify it, share it.