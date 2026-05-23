# End-to-End Test Flow

This document validates the complete career-automation system using a fictional user (Sarah Chen) and a fictional job posting (Trailhead Outdoors). Run through each test case and verify the expected output.

**Test corpus:** `tests/test-corpus/` contains pre-filled files for Sarah Chen.
**Sample JD:** `tests/sample-jd.md` contains the Trailhead Outdoors job posting.

---

## Test 1: State Detection — New User

**Setup:** Reset all files in `test-corpus/` to their `$PLACEHOLDER` template versions.

**Input:** User opens the agent (any first message).

**Expected behavior:**
- Agent reads PROFILE.md first, sees `$PLACEHOLDER` values
- Determines state = "not set up"
- Starts onboarding immediately (collects profile info, then builds corpus)
- Does NOT present a menu of options
- Does NOT ask "what would you like to do?"

**Validate:**
- [ ] Agent reads PROFILE.md and ACCOMPLISHMENTS.md first
- [ ] Agent detects placeholder state
- [ ] Agent starts collecting profile info (name, locations, roles, visa, etc.)
- [ ] Agent writes PROFILE.md with collected info
- [ ] Agent then builds ACCOMPLISHMENTS.md (from resume or conversation)

---

## Test 2: State Detection — Partially Set Up

**Setup:** PROFILE.md has real values, ACCOMPLISHMENTS.md has some placeholders.

**Input:** "I found this job at Trailhead Outdoors, should I apply?"

**Expected behavior:**
- Agent reads PROFILE.md — it's filled in
- Agent reads ACCOMPLISHMENTS.md — some gaps remain
- Agent checks whether the gaps block job scoring (they might not — current role might be enough)
- Proceeds with scoring, noting any data limitations

**Validate:**
- [ ] Agent reads both files
- [ ] Agent identifies what's missing
- [ ] If gaps block the action, agent asks for info first
- [ ] If gaps don't block, agent proceeds and notes limitations

---

## Test 3: Placeholder Audit — Missing Preferences

**Setup:** Reset PROFILE.md preferences to placeholder values (locations, roles, comp, visa).

**Input:** "I found this job at Trailhead Outdoors, should I apply?"

**Expected behavior:**
- Agent detects placeholder preference values in PROFILE.md
- Flags what's missing before scoring
- Asks for preferences naturally
- Does NOT silently score the job with incomplete preference data

**Validate:**
- [ ] Agent detects `$PLACEHOLDER` values in PROFILE.md
- [ ] Agent flags what's missing (locations, comp, visa)
- [ ] Agent asks before proceeding
- [ ] Score factors in preferences once provided

---

## Test 4: Job Scorer — Match Scoring

**Setup:** Use full Sarah Chen test corpus with all files filled in.

**Input:** The Trailhead Outdoors JD from `tests/sample-jd.md`

**Expected output:** A match report with:

```
## Job Match Report: Trailhead Outdoors — Senior Manager, Growth Analytics
```

**Validate against expected dimension scores:**

| Dimension | Expected Range | Reasoning |
|-----------|---------------|-----------|
| Skill Overlap | 15-19 | Strong on experimentation, analytics, SQL, attribution. Gap: predictive ML models |
| Seniority Fit | 14-18 | Senior Analyst → Senior Manager stretch, but doing the work |
| Domain Relevance | 16-20 | DTC e-commerce → DTC outdoor e-commerce, near-identical |
| Team/Scope Fit | 14-18 | Manages 4; JD wants 4-6, close match |
| Edit Effort | 14-18 | Moderate: reframe analyst→manager, add team leadership emphasis |

**Validate:**
- [ ] Preference Fit section present (location, comp, visa, role type vs PROFILE.md)
- [ ] All 5 dimensions scored with Notes
- [ ] Company research section present
- [ ] Recommendation clearly stated
- [ ] Entry added to APPLICATIONS-TRACKER.md

---

## Test 5: Resume Writer — Tailored Resume

**Input:** "Tailor my resume for the Trailhead Outdoors Senior Manager, Growth Analytics role"

**Expected output:** `resumes/RESUME-Trailhead-Outdoors-2026-05.md`

**Validate:**
- [ ] File in `resumes/` subfolder
- [ ] Contact header populated from PROFILE.md
- [ ] Summary reframed for growth analytics + team leadership
- [ ] Cascade bullets reordered (experimentation first)
- [ ] No fabricated skills or inflated claims
- [ ] Tailoring notes section exists showing what changed and why
- [ ] Gaps section honestly identifies the ML model gap
- [ ] No AI slop
- [ ] APPLICATIONS-TRACKER.md updated to `==Applied ✅==`

---

## Test 6: Interview Prep — Prep Packet

**Input:** "I have an interview at Trailhead Outdoors for the Senior Manager, Growth Analytics role. Hiring manager round."

**Expected output:** `INTERVIEW-PREP-Trailhead-Outdoors-2026-05.md`

**Validate:**
- [ ] Company context section present
- [ ] Behavioral questions mapped to Sarah's best stories
- [ ] Technical questions flagged (SQL, experiment design, LTV)
- [ ] Gap areas section (ML models, product analytics)
- [ ] Top 5 stories quick reference
- [ ] Questions to ask the HM (specific, not generic)
- [ ] Salary expectations sourced from PROFILE.md
- [ ] APPLICATIONS-TRACKER.md updated to `==Interviewing 🔄==`

---

## Test 7: Corpus Builder — Adding a New Win

**Input:** "I just got promoted to Manager, Growth Analytics at Cascade. My team grew to 6 people and I'm now presenting to the C-suite monthly."

**Validate:**
- [ ] ACCOMPLISHMENTS.md updated with new title, team size, C-suite detail
- [ ] MASTER-RESUME.md updated with new title and expanded bullets
- [ ] Previous title preserved (shows progression)

---

## Test 8: Anti-AI-Slop Validation

Scan ALL generated outputs for banned patterns. Any hit = FAIL.

| Pattern | Check |
|---------|-------|
| "pivotal" | grep all output files |
| "testament" | grep all output files |
| "leveraged" as verb | grep all output files |
| "synergies" | grep all output files |
| "vibrant landscape" | grep all output files |
| "spearheaded" | grep all output files |
| "utilize" | grep all output files |
| Em dashes (—) | max 2 per file |
| Rule of three | "built, scaled, and optimized" style |

---

## Test 9: Corpus Integrity Check

After all tests, verify the **corpus remains the source of truth**:

- [ ] ACCOMPLISHMENTS.md updated before MASTER-RESUME.md
- [ ] No info in a resume that isn't in ACCOMPLISHMENTS.md
- [ ] Tailoring notes reference specific corpus entries
- [ ] Interview prep stories match INTERVIEW-BANK.md
- [ ] APPLICATIONS-TRACKER.md consistent with all the above
- [ ] PROFILE.md is the sole source for contact info and preferences (not duplicated)

---

## Running the Tests

### Automated validation script

```bash
cd tests

# Check that all required files exist
for f in test-corpus/PROFILE.md test-corpus/ACCOMPLISHMENTS.md test-corpus/MASTER-RESUME.md test-corpus/INTERVIEW-BANK.md test-corpus/APPLICATIONS-TRACKER.md sample-jd.md; do
  if [ -f "$f" ]; then echo "✓ $f exists"; else echo "✗ $f missing"; fi
done

# Anti-AI-slop check on test corpus
echo ""
echo "=== Anti-AI-Slop Check on Test Corpus ==="
for word in pivotal testament synergies vibrant spearheaded utilize orchestrated fostered; do
  count=$(grep -ri "$word" test-corpus/ 2>/dev/null | wc -l | tr -d ' ')
  if [ "$count" = "0" ] || [ -z "$count" ]; then echo "✓ '$word' not found"; else echo "✗ '$word' found $count times"; fi
done

# Check em dash usage
for f in test-corpus/*.md; do
  count=$(perl -0777 -pe 's/<!--.*?-->//gs' "$f" | grep -o '—' | wc -l | tr -d ' ')
  if [ "$count" -gt 2 ]; then echo "✗ $(basename $f) has $count em dashes (max 2)"; else echo "✓ $(basename $f) em dashes OK ($count)"; fi
done
```

### Manual flow validation

1. Point the agent at `tests/test-corpus/` as the user's career folder
2. Feed each test input from this document
3. Verify each output against the checklist

---

## Test Results Template

| Test | Status | Notes |
|------|--------|-------|
| Test 1: New User State Detection | ⬜ | |
| Test 2: Partial Setup State Detection | ⬜ | |
| Test 3: Placeholder Audit | ⬜ | |
| Test 4: Job Scorer | ⬜ | |
| Test 5: Resume Tailoring | ⬜ | |
| Test 6: Interview Prep | ⬜ | |
| Test 7: Corpus Update | ⬜ | |
| Test 8: Anti-AI-Slop | ⬜ | |
| Test 9: Corpus Integrity | ⬜ | |