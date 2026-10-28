# Step 5 — Human in the Loop

> "Talent team reviews the bulk of the profiles. ~20% pass. Hiring Manager does a second review and passes around 10-20%."
> "Just keep it simple, it's on a Google Sheet."

---

## The two-stage human review

### Stage 1 — Talent team review
- Review ALL profiles that passed the AI evaluate step (Tier A and B)
- Target pass rate: ~20%
- What you are looking for: does this profile feel right for the role, the team, the moment?
- This is judgment, not just criteria-checking

### Stage 2 — Hiring Manager review
- Share only Stage 1 passes with the Hiring Manager
- Target pass rate: 10–20% of what you shared
- HM is looking for: culture fit, specific experience, team dynamics
- Keep the list to 20–30 profiles maximum per review session

---

## The Google Sheet tracker (keep it simple)

Bence explicitly said: "Just keep it simple, it's on a Google Sheet."

### Columns

```
A: Full Name
B: LinkedIn URL
C: Portfolio / GitHub URL
D: Current Title
E: Current Company
F: Location
G: Primary Signal Source (where you found them)
H: AI Score (from evaluate step)
I: AI Tier (A/B/C/Pass)
J: AI Standout Signal
K: Talent Review (Yes / No / Maybe)
L: Talent Review Notes
M: HM Review (Yes / No / Maybe)
N: HM Review Notes
O: Status (Not contacted / Outreach sent / Replied / Interview / Hired / Declined / Pass)
P: Outreach Date
Q: Last Touch Date
R: Next Action
```

### Colour coding (apply conditional formatting)

| AI Tier | Colour |
|---|---|
| A (75-100) | Dark green |
| B (50-74) | Light green |
| C (25-49) | Yellow |
| Pass (0-24) | Grey |

| Status | Colour |
|---|---|
| Hired | Dark green |
| Interview | Light green |
| Replied | Blue |
| Outreach sent | Light blue |
| Declined | Red |
| Pass | Grey |

---

## How to run the Talent Review (Stage 1)

Set aside 2 hours per role. Work through the sheet systematically:

1. Sort by AI Score descending
2. For each Tier A profile: open their LinkedIn and portfolio in two tabs
3. Spend max 3 minutes per profile
4. Mark K (Talent Review) as Yes / No / Maybe
5. For Yes: write one sentence in L explaining why
6. For No: write one phrase (e.g. "too senior", "wrong domain", "agency not product")
7. Move through all Tier B after completing Tier A

**Target time:** 3 minutes per profile. 60 profiles = 3 hours maximum.

---

## How to run the HM Review (Stage 2)

Share a filtered view of the sheet with only Talent Review = Yes profiles.

Before the HM review session:
- Filter to Talent Review = Yes
- Sort by AI Score descending
- Add a column: "Why I'm showing you this" — one sentence per profile

In the HM review session (30–45 minutes):
- Walk through profiles together, not async
- For each: show LinkedIn, show portfolio
- HM marks M (HM Review) as Yes / No / Maybe in real time
- Capture the NO reasons — these calibrate future searches

**The most important question to ask the HM:** "Which of these is closest to what you had in mind, and which is furthest? Tell me why for both." Their answer recalibrates your sourcing.

---

## Data hygiene for the sheet

### What must never be empty
- Column A (Full Name)
- Column B (LinkedIn URL)
- Column G (Signal Source)
- Column K or M (at least one review column must be filled before outreach)

### Weekly maintenance (10 minutes)
- Update Column O (Status) for anyone who replied
- Update Column Q (Last Touch Date)
- Fill Column R (Next Action) for anyone in active stages

### Monthly maintenance (30 minutes)
- Archive all Pass profiles to a separate tab (keep for future roles)
- Review No reasons from HM — are there patterns? Update your evaluate criteria.
- Check if any Maybe profiles should be moved to Yes now that time has passed

