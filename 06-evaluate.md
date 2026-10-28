# Step 4 — Evaluate

> "The more you can automate this step, the more scalable your solution will be."

---

## Three levels of evaluation sophistication

Bence showed three levels. Start at Level 1. Move to Level 2 when you have enough data.
Only attempt Level 3 if you have a data team.

### Level 1 — Hard-coded criteria
A list of hard-coded criteria (e.g. is an individual, staff+ level, etc.)

**What it is:** A simple checklist. Binary pass/fail on each criterion.
**When to use:** First version of any new role. Build this in a day.
**Limitation:** Does not weight signals. Does not learn.

**Example for a Senior Engineer:**
```
Must have ALL of these (hard pass/fail):
- is_individual = true
- relevant = yes
- seniority = senior OR staff OR principal
- primary_language matches role requirement
- last GitHub activity within 6 months
- Has at least 1 repo with 10+ stars OR contributed to a known OSS project

Nice to have (bonus points, not required):
- 50+ GitHub followers
- Contributed to repos in our target domain
- Has a personal blog or has given a talk
```

### Level 2 — Multi-signal overlay
Overlay multiple signals (target companies, online presence, quality of work, etc.)

**What it is:** Weighted scoring across multiple dimensions.
**When to use:** After your first 20–30 hires when you know which signals matter.
**Limitation:** Still rule-based. Weights are your best guess until you have outcome data.

**Example scoring rubric:**
```
Signal                          Weight    How to measure
---                             ---       ---
Works/worked at target company   25%      Company list from intake
OSS contribution depth           20%      Stars received + merged PRs
Recency of activity              20%      Last commit date
Social reach in domain           15%      Followers on most relevant platform
Portfolio/work quality           10%      Manual review (human step)
Seniority match                  10%      Classifier output

Total: 100%

Score 0-100. Threshold for human review: 60+
Threshold for direct outreach: 80+
```

### Level 3 — ML model
An ML model figures out the relevant signals and their weights (e.g. logistic regression).

**What it is:** Train a model on your past hiring outcomes to predict which profiles convert.
**When to use:** You have 50+ hires with outcome data. You have a data team. Not before.
**Limitation:** Requires significant data and engineering resources. Do not attempt this until Levels 1 and 2 are working well.

---

## Practical Level 2 evaluation prompt

Use this after enrichment and classification. Feed it the enriched + classified JSON:

```
You are evaluating a candidate profile for a [role_title] role at [company].

Role requirements:
[paste your intake rubric here]

Target companies (highest signal):
[list 10-15 target companies]

Candidate profile:
{EnrichmentData + ClassificationData JSON}

Score this candidate 0-100 across these dimensions:

1. Company signal (0-25 points)
   - Currently at or recently left a target company: 25
   - At a strong adjacent company: 15
   - At a relevant but lower signal company: 8
   - Company not relevant: 0

2. Expertise depth (0-25 points)  
   - Strong public evidence of deep expertise (OSS, publications, talks): 25
   - Some public evidence: 15
   - No public evidence but strong company signal: 8
   - No evidence: 0

3. Activity recency (0-25 points)
   - Active in last 30 days: 25
   - Active in last 90 days: 18
   - Active in last 6 months: 10
   - Inactive over 6 months: 0

4. Community reach (0-25 points)
   - 500+ followers on most relevant platform: 25
   - 100-499 followers: 15
   - 20-99 followers: 8
   - Under 20 or no presence: 0

Return JSON ONLY:
{
  "total_score": <0-100>,
  "tier": "<A|B|C|Pass>",
  "company_score": <0-25>,
  "expertise_score": <0-25>,
  "activity_score": <0-25>,
  "reach_score": <0-25>,
  "standout_signal": "<one specific thing worth highlighting>",
  "concern": "<one concern if any, otherwise empty string>",
  "recommended_action": "<outreach_now|add_to_pool|pass>"
}

Tier definitions:
A = 75-100: Strong signal, reach out now
B = 50-74: Good signal, add to talent pool
C = 25-49: Weak signal, monitor
Pass = 0-24: Not relevant
```

---

## How to calibrate your evaluation

Run your first 20 profiles through the Level 2 prompt. Then:

1. Have a human (you) review all 20 and mark which ones you would actually reach out to
2. Compare your human judgment to the AI scores
3. Find the disagreements — where did AI score high but you said no? Where low but you said yes?
4. Update the prompt criteria based on what you learn
5. Repeat after every 20 profiles

**Target:** 80%+ agreement between AI score and your human judgment after 4–5 calibration rounds.

