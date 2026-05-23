# Interview Bank

STAR stories, behavioral answers, and technical prep. Add to it after every interview.

---

## Tell Me About Yourself (90 seconds)

> $YOUR_INTRO_PARAGRAPH
> - State level, domain, and years
> - Name your flagship accomplishment at current company
> - Connect to what draws you to the next role
> - Tailor the last sentence per interview

---

## STAR Stories

### Story: $STORY_NAME
**Tags:** #$TAG1 #$TAG2 #$TAG3
**Source Role:** $TITLE @ $COMPANY

**Situation:**
> $CONTEXT_AND_PROBLEM

**Task:**
> $WHAT_YOU_NEEDED_TO_DO

**Action:**
> $SPECIFIC_STEPS_YOU_TOOK

**Result:**
> $QUANTIFIED_OUTCOME

**Use for:**
- "$RELATED_QUESTION_1"
- "$RELATED_QUESTION_2"

---

## Technical Prep

### SQL Pre-Flight Checklist

Before submitting any SQL answer in an interview:

1. **Syntax scan:** read every line, check commas, spell table/column names
2. **JOIN audit:** for every JOIN, ask "what happens to rows that don't match?"
3. **Window function check:** if using OVER(), ask "what's my PARTITION BY?"
4. **Grain verification:** what's one row in my output? Does GROUP BY match?
5. **Mental trace:** pick example data and walk through the logic

### Common SQL Patterns

| Pattern | When to Use | Template |
|---------|------------|----------|
| Rank within group | "Top N per category" | `ROW_NUMBER() OVER(PARTITION BY cat ORDER BY val DESC)` |
| Running total | "Cumulative sum" | `SUM(val) OVER(ORDER BY date)` |
| Period-over-period | "Month over month change" | `LAG(val) OVER(ORDER BY date)` |
| Retention/cohort | "% returning users" | Self-join on user_id with date offset |

### Framework Questions

- **Metric definition:** State it once upfront, lock it, don't change mid-answer
- **Clarifying questions:** Always ask scope before diving in (time window, user definition, success criteria)
- **Experimentation design:** Randomization unit, treatment, control, primary metric, guardrail metrics, runtime

---

## Behavioral Q&A

| Question | Best Story | Key Deliverable |
|----------|-----------|-----------------|
| "Tell me about your biggest accomplishment" | $STORY_NAME | $ONE_SENTENCE_THAT_MUST_LAND |
| "Tell me about a time you dealt with conflict" | $STORY_NAME | $ONE_SENTENCE_THAT_MUST_LAND |
| "Tell me about a failure" | $STORY_NAME | $ONE_SENTENCE_THAT_MUST_LAND |
| "How do you influence without authority?" | $STORY_NAME | $ONE_SENTENCE_THAT_MUST_LAND |
| "Tell me about a time you built a team" | $STORY_NAME | $ONE_SENTENCE_THAT_MUST_LAND |

---

## Interview Debriefs

After each interview, add:

### $COMPANY, $ROLE ($DATE)
**Round:** $ROUND_TYPE
**Result:** $OUTCOME
**What went well:** $NOTES
**What went wrong:** $NOTES
**Key lesson:** $ONE_THING_TO_FIX