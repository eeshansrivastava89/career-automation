---
name: job-scorer
version: 1.2.0
description: |
  Score a job posting for fit. Fetches the JD, scores across 5 dimensions +
  preference match, researches the company, gives an apply/skip recommendation.
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
  - fetch_content
---

# Job Scorer

Score whether a job posting is worth the user's time.

## Prerequisites

Read `my-career/PROFILE.md` and `my-career/ACCOMPLISHMENTS.md` before starting. If either has placeholder values that block scoring (locations, roles, visa, current role), ask the user to fill them first. Don't score on incomplete data.

## Step 1: Get the JD

**URL provided:** Fetch with `web_fetch` or `fetch_content`. If blocked (403, paywall), ask the user to paste the text.

**Text pasted:** Use directly.

**Vague reference:** Search with `web_search`, confirm the match.

## Step 2: Extract JD Requirements

Parse the JD for: title, company, location, comp, visa sponsorship, required skills, preferred skills, scope signals, seniority, domain, key responsibilities.

## Step 3: Check Against User Preferences

Read `my-career/PROFILE.md` and compare:

| JD has | Check against |
|--------|--------------|
| Location | Target locations |
| Title | Target roles |
| Comp range | User's comp range |
| Visa language | User's visa needs |

Surface mismatches in the report.

## Step 4: Score the Match (5 dimensions, 0-20 each)

**Skill Overlap:** How directly do the user's skills match the JD's required skills?
- 16-20: 80%+ overlap at professional scale
- 11-15: 50-80%, some adjacent but not direct
- 6-10: Significant gaps
- 0-5: Minimal overlap

**Seniority Fit:** Does the user's level match the role's level?
- 16-20: Exact level match
- 11-15: One level off (stretch but realistic)
- 6-10: Two+ levels off
- 0-5: Fundamentally mismatched

**Domain Relevance:** How relevant is the user's industry/business model experience?
- 16-20: Same industry, same model
- 11-15: Adjacent domain
- 6-10: Different domain, transferable skills
- 0-5: No relevant experience

**Team/Scope Fit:** Does the user's experience match the role's scope?
- 16-20: Similar team size, scope, stakeholder level
- 11-15: Close — slightly smaller or different mix
- 6-10: Significant gap
- 0-5: Fundamentally different org experience

**Resume Edit Effort** (inverted): How much work to make the resume competitive?
- 16-20: Minimal edits needed
- 11-15: Moderate — reframe 2-3 bullets
- 6-10: Heavy — significant reframing needed
- 0-5: Would need to misrepresent background

**Total → Recommendation:**
| Score | Recommendation |
|-------|---------------|
| 85-100 | **Apply** |
| 70-84 | **Apply if interested** |
| 55-69 | **Stretch** |
| 0-54 | **Skip** |

## Step 5: Research the Company

`web_search` for: what they do, financial health, employee sentiment, org context, risks (layoffs, restructuring, declining growth).

## Step 6: Output the Report

```markdown
## Job Match Report: [Company] — [Title]

**Match Score: [X]/100 — [Recommendation]**

### Preference Fit
- **Location:** [Match/mismatch]
- **Comp:** [Listed range vs. user's target, or "not listed"]
- **Visa:** [Offered vs. needed]
- **Role type:** [Matches/adjacent to user's targets]

| Dimension | Score | Notes |
|-----------|-------|-------|
| Skill Overlap | /20 | ... |
| Seniority Fit | /20 | ... |
| Domain Relevance | /20 | ... |
| Team/Scope Fit | /20 | ... |
| Edit Effort | /20 | ... |

### Company Profile
- **What they do:** ...
- **Financial health:** ...
- **Risks:** ...

### Recommendation: [Apply / Apply if interested / Stretch / Skip]

**Pros:** ...
**Cons/Risks:** ...

### Resume Edit Direction
1. ...
2. ...
```

## Step 7: Record It

Add to `my-career/APPLICATIONS-TRACKER.md`:

```markdown
| [Company] | [Title] | [Score] | ==Scored 📊== | [Month Year] | [1-line summary] |
```

## Rules

1. **Be honest.** A high score for a bad fit wastes the user's time.
2. **Show your work.** Every dimension needs a Notes explanation.
3. **Don't oversell.** "Skip" on a marginal role is the right call.
4. **Flag visa risk.** If the user needs sponsorship and the JD is silent, call it out.
5. **Always research the company.** Even a 90-match role might be at a company doing layoffs.
6. **Check preferences first.** Score on incomplete preferences is unreliable.