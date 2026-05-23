<div align="center">

# Career Automation

**Build your career corpus once, score job fits, tailor resumes, prep for interviews — all from one folder.**

[![license](https://img.shields.io/github/license/eeshansrivastava89/career-automation)](LICENSE)
[![platform](https://img.shields.io/badge/platform-Claude%20Code%20%7C%20Codex%20%7C%20Pi%20%7C%20OpenCode-blue)]()

</div>

<br>

**Open your AI agent in this folder.** That's it. There's no install command, no terminal setup, no scripts. The agent reads `AGENTS.md`, sees your files are empty, and walks you through setup.

```bash
git clone https://github.com/eeshansrivastava89/career-automation.git
cd career-automation
# Then open this folder in Claude Code, Codex, Pi, or OpenCode
```

> **Requirements:** An AI agent that supports custom project instructions (Claude Code, Codex, Pi, OpenCode, etc.) and a text editor for your career files. No code, no terminal, no LaTeX.

## What it does

Most AI resume tools are single-shot: paste a JD, get a generic resume. This system is **corpus-driven**. You answer questions about your career once, and every output after that — match scores, tailored resumes, interview prep — derives from that knowledge base. The more you add, the smarter it gets about you.

The agent decides what to do based on **what's in your files**, not from parsing what you type. Empty files? It onboards you. Partial info? It fills the gaps. Ready to go? It acts on whatever you ask for.

| | |
|---|---|
| **Corpus-driven** | Build your career knowledge base once. Every output derives from it. |
| **Job scoring** | 5-dimension match score + preference fit + company research. Clear apply/skip call. |
| **Tailored resumes** | One command, clean markdown resume tailored to a specific role. Truthful emphasis, not keyword stuffing. |
| **Interview prep** | STAR stories mapped to likely questions, gap flags, company-specific prep packets. |
| **Resume import** | Drop a PDF in `my-career/`, the agent extracts it and builds your corpus. |
| **Anti-AI-slop** | Banned word lists, "read it aloud" checks, no "pivotal," "testament," "leveraged synergies." |

## How it works

```
SET UP:      Fill PROFILE.md + build career corpus (one-time, ~15 min)
EVALUATE:    Paste a job posting → get a match score + company research
APPLY:       One command → tailored markdown resume from your real accomplishments
PREPARE:     Get interview → company-specific prep packet with your best stories
ITERATE:     Add wins, track outcomes, get smarter over time
```

State is file-driven, not command-driven:

| Your files | What the agent does |
|-----------|-------------------|
| Empty (placeholders) | Starts onboarding — points you to PROFILE.md, asks about your resume |
| Partially filled | Fills gaps before taking action, asks for what's missing |
| Fully filled | Does whatever you ask — score a job, write a resume, prep for an interview |

## Match scoring

Every job is scored across 5 dimensions (0-20 each) plus a preference fit check:

| Dimension | Measures |
|-----------|----------|
| Skill Overlap | How directly your skills match the JD |
| Seniority Fit | Whether your level matches the role |
| Domain Relevance | How relevant your industry experience is |
| Team/Scope Fit | Whether your leadership experience matches the scope |
| Edit Effort | How much resume rework is needed (inverted) |

| Score | Recommendation |
|-------|---------------|
| 85-100 | Apply |
| 70-84 | Apply if interested |
| 55-69 | Stretch |
| 0-54 | Skip |

Every score comes with reasoning you can audit. The agent doesn't just say "apply" — it shows why.

## Folder structure

```
career-automation/
├── AGENTS.md                    ← Agent reads this first
├── skills/                      ← System instructions (don't edit)
│   ├── corpus-builder/SKILL.md     Onboarding + corpus management
│   ├── job-scorer/SKILL.md         JD → match score → recommendation
│   ├── resume-writer/SKILL.md      Tailored resume generation
│   └── interview-prep/SKILL.md    Interview prep packets
└── my-career/                   ← Your career files (the agent fills these)
    ├── PROFILE.md                  Contact info + job preferences
    ├── ACCOMPLISHMENTS.md          Career corpus (single source of truth)
    ├── MASTER-RESUME.md            Baseline resume
    ├── INTERVIEW-BANK.md           STAR stories + technical prep
    ├── APPLICATIONS-TRACKER.md     Job search pipeline
    └── resumes/                    Tailored resume outputs
```

You only need to care about `my-career/`. Everything else is system files.

## License

[MIT](LICENSE)