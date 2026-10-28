# The 7-Step Sourcing Flywheel

> Bence Gedai's core framework from ElevenLabs.
> "Build a self-reinforcing flywheel — the more high target profiles you find, the more signals you have to identify new ones."

---

## The flywheel diagram

```
                    1. SIGNALS
                   /           \
          7. REACH OUT         2. ENRICHMENT
         /                              \
  6. TALENT POOL                    3. CLASSIFY
         \                              /
          5. HUMAN IN THE LOOP    4. EVALUATE
                   \           /
                    (continue)
```

Each step feeds the next. The flywheel gets stronger every cycle because:
- Step 6 (talent pool) feeds better signals back into Step 1
- Step 5 (human review) calibrates Step 4 (evaluate) over time
- Step 3 (classify) gets more accurate as you add more role context

---

## Overview of all 7 steps

| Step | Name | What happens | AI or human? |
|---|---|---|---|
| 1 | Signals | Identify where to find candidates | Human decides, AI executes |
| 2 | Enrichment | Find all relevant online signals for each profile | AI (LLM + web search) |
| 3 | Classify | Route profile to the right role | AI |
| 4 | Evaluate | Score the profile against your criteria | AI (3 levels of sophistication) |
| 5 | Human in the loop | Talent team reviews, ~20% pass | Human |
| 6 | Talent pool | Store high-signal profiles for future outreach | System |
| 7 | Reach out | Contact shortlisted candidates | Human (with AI assist) |

---

## How to run the flywheel in practice

### Frequency
- Run a full cycle every 2–4 weeks per active role
- Step 6 (talent pool) is refreshed every quarter
- Step 1 (signals) is updated every time you find a new source

### The self-reinforcing loop
When you finish one cycle and store profiles in Step 6:
1. Look at the highest-rated profiles in your talent pool
2. Ask Claude: "I have these 10 high-signal profiles. Find me 20 more people similar to them." (look-alike search)
3. Feed the results back into Step 1 as a new signal source
4. Your pool gets better quality every cycle

### What each role needs
- **Engineering roles:** GitHub contributor lists as primary signal source
- **Design roles:** Dribbble, Behance, Figma Community, Read.cv
- **Product roles:** Substack, ProductHunt, Lenny's Slack, conference speaker lists
- **GTM roles:** Apollo, newsletter credits, conference speakers, community forums

