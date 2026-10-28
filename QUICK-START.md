# Quick Start Guide

> Read this first. Everything else is reference material.
> This tells you exactly what to do on Day 1, Week 1, and Month 1.

---

## Day 1 — Read and decide (2 hours)

**Step 1 — Read 01-build-vs-buy.md**
Answer this question honestly: Is automation worth it for your current role?
- If no active roles are niche, high-volume, or in saturated markets → use your existing stack and come back to this repo in 4 weeks
- If yes → continue

**Step 2 — Read 02-framework-flywheel.md**
Understand the 7-step loop. Draw it on paper. Know which step each file covers.

**Step 3 — Pick your first role to run the framework on**
Choose a role that is:
- Currently active (not hypothetical)
- Either niche, volume (3+), or showing low response rates with conventional sourcing
- One where you are the primary recruiter (no dependencies on others to start)

---

## Week 1 — Build the foundation (10 hours)

### Day 1–2: Context Pack (2 hours)
Open 12-prompts-library.md → find prompt CP1
Paste your role brief into Claude with that prompt.
Review the output. Fix anything wrong. Save as a Google Doc titled:
`[Role Title] — Context Pack v1.0 — [Date]`

This document will feed every other step. Do not skip it.

### Day 3: Signal sources (2 hours)
Open 03-signals.md
Run prompt S1 (Generate sourcing ideas) with your role type.
From the output, pick the top 3 signal sources.
For each: open the URL and manually pull 20–30 profiles. 
Add to your Google Sheet (see 07-human-in-the-loop.md for column structure).

### Day 4: Enrichment (2 hours)
Open 04-enrichment.md
For your 20–30 profiles: decide between Claude web search vs Clay vs Apollo.
Run enrichment on each profile. Add results to your sheet.
Do NOT move to classify until you have enriched at least 15 profiles.

### Day 5: Classify + Evaluate (2 hours)
Open 05-classify.md → pick the classifier for your role type
Run each enriched profile through the classifier. Add output to sheet.
Filter to: relevant = yes AND is_individual = true
Open 06-evaluate.md → run EV1 on all remaining profiles
Add scores and tiers to sheet. Sort by total_score descending.

### Day 6–7: Human review + outreach (2 hours)
Open 07-human-in-the-loop.md
Review all Tier A and B profiles yourself. Mark Yes / No / Maybe.
For every Yes: write one sentence in your Notes column on why.
Write outreach for the top 5 Yes profiles using prompt O1 from 12-prompts-library.md.
Send or schedule the messages.

**End of Week 1 target:**
- Context Pack complete
- 20–30 profiles sourced
- 15+ profiles enriched and classified
- 10+ profiles evaluated
- 5+ outreach messages sent

---

## Week 2 — Calibrate and iterate (5 hours)

### HM calibration session
Open 11-talent-one-context-pack.md → find prompt CAL1
Run it with your Context Pack. Share the output with your hiring manager.
Run the calibration session (30 minutes). Record what you learn.
Update your Context Pack with any corrections.

### First calibration review
Look at your first 10 evaluated profiles.
For each Tier A you marked No in human review: why? What did the AI miss?
For each Tier C or Pass you marked Yes: why? What signal did the AI underweight?
Update your EV1 prompt with what you learned.
Note changes in a "Prompt changelog" section at the bottom of your sheet.

### Send follow-ups
For anyone who did not reply to Week 1 outreach: send the Day 6 follow-up from 09-reach-out.md

---

## Month 1 — Run the full flywheel (ongoing)

### Week 3
Add a second signal source. Run it through the full pipeline.
Compare quality: which signal source is producing better Tier A profiles?
Add your first profiles to the Talent Pool tab (see 08-talent-pool.md).

### Week 4
Review your reply rates from outreach.
If below 15%: re-read 09-reach-out.md. Review your messages. What is generic?
If above 25%: your signal sources and messages are working. Scale the same approach.
Run the weekly calibration ritual: 15 minutes reviewing AI vs human disagreements.

### End of Month 1 targets
- 2–3 signal sources active
- 50+ profiles evaluated
- 15–20 profiles in human review
- 8–10 profiles in HM review
- 5–8 outreach conversations active
- Talent pool seeded with 10+ profiles
- Evaluation prompt updated at least twice based on calibration

---

## The one habit that makes everything else work

Every Friday, spend 15 minutes on this:

```
1. Open your sheet
2. Pick 5 profiles where AI and human disagreed
3. Ask: "Why was the AI wrong?"
4. Update one thing in your evaluation prompt
5. Log the change in your prompt changelog
```

This 15-minute weekly ritual is what turns a static system into a learning one.
After 8 weeks of doing this, your evaluation accuracy will be dramatically better 
than week 1. After 6 months, your prompt will be calibrated to your specific market, 
your specific companies, and your specific hiring bar in a way no off-the-shelf tool can replicate.

---

## If you get stuck

| Problem | Where to look |
|---|---|
| Not finding enough profiles | 03-signals.md → try a different signal type |
| Finding many profiles but none are right | 01-build-vs-buy.md → are you using the right signal source for this role? |
| AI evaluation disagrees with your judgment | 06-evaluate.md → calibration section |
| HM keeps rejecting profiles you thought were strong | Run the CAL1 calibration prompt. Your WGLL is wrong. |
| Low reply rates to outreach | 09-reach-out.md → check your opening line. Is it specific enough? |
| Talent pool not converting on re-engagement | 08-talent-pool.md → check timing and personalise the re-engagement message |

