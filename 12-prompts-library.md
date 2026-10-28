# Prompts Library — All Prompts, Copy-Paste Ready

> Every prompt from this framework in one place.
> Replace all [bracketed] text with your specifics before using.

---

## SIGNAL PROMPTS

### S1 — Generate sourcing ideas
```
You're a talent engineer. Do a deep research, build me a comprehensive list 
of ideas to gather signals online for strong [designers/engineers/PMs/GTM professionals], 
e.g. awards, jury member, podcast speakers, newsletter contributors, community leaders, 
conference speakers, etc. 

Be very specific about platform types and concrete platforms. 
Gather your findings in a table with these columns: 
- Type (award/community/conference/publication/etc.)
- Concrete source (specific URL or platform name)
- Signal strength prediction (high/medium/low)
- Implementation difficulty to automate (easy/medium/hard)
- How to access the list of names (specific action)
```

### S2 — Pull list of people from a website
```
Check [target website URL], search online, go through website references and case studies 
to build a comprehensive list of all the [video editors / designers / engineers / writers] 
who currently or in the past worked there.

For each of these people, do a separate web search. Find me:
- Their full name
- Job title
- Location / country
- LinkedIn URL
- Portfolio or personal website URL
- Most active social media URL (Instagram, Dribbble, GitHub, X — whichever is most relevant)

Make sure to only link URLs if you are certain they belong to the same person.
Write your outputs in TSV format with headers.
```

### S3 — Pull list from a newsletter or publication
```
Review the first 5 pages at: [target newsletter URL]

Review all the agencies and individuals featured in these listings.

As an output, give me:
- TSV 1: All agencies (name, location, predicted size, LinkedIn URL, website URL, relevant social links)
- TSV 2: All individuals

For individuals try to find their LinkedIn page, website and social links 
(Instagram, X, Dribbble, Behance, GitHub etc.) — highlight the one where they're most active.
Also find their job title and location.
```

### S4 — Look-alike search from talent pool
```
Do a deep research based on profiles I have already identified as high targets.
Find me similar people and return them in TSV format.

Here are my high-target profiles:
[paste names, titles, companies, and one sentence on why each is strong]

For each new profile you find:
- Full name
- Current title
- Current company
- LinkedIn URL
- Why they are similar to my targets (one sentence)
- Where you found them

Find 20 new profiles. Prioritise quality over quantity.
```

### S5 — Network discovery
```
These 3 people are strong signals for the type of [role] I am hiring for:

[Profile 1: Name, Title, Company, LinkedIn]
[Profile 2: Name, Title, Company, LinkedIn]
[Profile 3: Name, Title, Company, LinkedIn]

Map their professional networks to find where they intersect.
Tell me:
1. What conferences do all three attend or speak at?
2. What communities (Slack, Discord, forums) are they likely members of?
3. What newsletters or publications do they contribute to or follow?
4. Who in their LinkedIn networks appears multiple times across all three profiles?
5. What OSS projects or public work do they engage with?

Give me 5 specific sourcing actions I can take based on this network map.
```

---

## ENRICHMENT PROMPTS

### E1 — Full enrichment prompt (Bence's version)
```
You are an OSINT research assistant.
Input: a single token that we KNOW belongs to the person of interest:
URL: [paste the profile URL]
Username/handle: [paste the username if different]

This input is ground truth. Everything you return must describe THIS person.

Your task is enrichment only. Collect factual data points. Do not evaluate, 
classify, rate or judge the person in any way.

1. Search the web and open the input profile to establish who this person is.
2. Find their full name.
3. Find their personal website or portfolio URL.
4. Find their profiles on: LinkedIn, GitHub, Dribbble, Behance, Instagram, X.
5. Find the follower count on each platform where you found a profile.
   Return a single integer best-estimate per platform (no commas, no ranges, 
   no k/m suffix — e.g. 12500). Do NOT use the X/Twitter API.

IDENTITY MATCHING — most important rule:
Only return a profile link when you have positive evidence it is the SAME PERSON.
Acceptable evidence: profile is linked from the input profile's bio; from their 
personal website; from another confirmed profile; shows same full name AND matching 
context (same employer, same city, same conference bio).
A matching username alone is NOT evidence. Neither is a common name alone.

If two or more different people plausibly own a profile, return an empty string.
Never construct or guess a URL. Empty string when not confident.

Return JSON ONLY:
{
  "name": "",
  "website": "",
  "x_url": "",
  "linkedin_url": "",
  "instagram_url": "",
  "github_url": "",
  "dribbble_url": "",
  "behance_url": "",
  "x_followers": "",
  "linkedin_followers": "",
  "instagram_followers": "",
  "github_followers": "",
  "dribbble_followers": "",
  "behance_followers": ""
}
```

---

## CLASSIFY PROMPTS

### C1 — Designer classifier (Bence's version)
```
You are a talent-sourcing analyst.
Input: enriched profile data for a single person (JSON):
[paste EnrichmentData JSON here]

This data is ground truth. Do not look for new profiles or change any input values.
Your task is evaluation only. Use the input data plus linked profiles to judge the person.

1. Department: pick best fit from: Product, Design, Engineering, Sales, Marketing, 
   Support, Content, Consumer, Artist, Writer, Research.

2. Relevant (yes/no): is this person relevant for Designer roles (Product Designer, 
   Website Designer, Creative Director, Brand Designer, Founding Designer or similar) 
   or Engineering-related roles? Developer relations/advocate count as relevant. 
   Product managers and CPOs do not.

3. Seniority: junior, senior, staff, or director.

4. Category: the kind of designer they are. Pick only one: website, mobile, advocate, 
   motion, branding, product, vr/ar, 3D, creative director, producer, etc.
   If no category fits, return a new value.

5. Is individual: false for companies/studios/agencies, true only for individuals.

Rules:
- Base every judgment on evidence from the input data and linked profiles.
- Use web search only to read already-linked profiles, not to find new ones.
- If evidence is insufficient, return empty string. Do not guess.
- Return "relevant" as "yes" or "no" (lowercase).
- Use only allowed values for department and seniority.

Return JSON ONLY:
{
  "department": "",
  "relevant": "",
  "seniority": "",
  "category": "",
  "is_individual": false
}
```

### C2 — Engineering classifier
```
You are a talent-sourcing analyst.
Input: enriched profile data for a single person (JSON):
[paste EnrichmentData JSON here]

This data is ground truth. Do not look for new profiles or change any input values.

1. Department: Backend Engineering, Frontend Engineering, Platform/Infra, ML/AI Engineering, 
   Data Engineering, Full Stack, DevOps/SRE, Other Engineering, Not Engineering.

2. Relevant (yes/no): relevant for [paste role description in one sentence]?

3. Seniority: junior, mid, senior, staff, principal, director.

4. Primary language: Go, Python, Java, Rust, TypeScript, JavaScript, Scala, C++, Other.

5. Signal strength: strong / medium / weak 
   (based on OSS contributions, GitHub activity, public work).

6. Is individual: false for companies/recruiters, true only for individual engineers.

Rules: same as above.

Return JSON ONLY:
{
  "department": "",
  "relevant": "",
  "seniority": "",
  "primary_language": "",
  "signal_strength": "",
  "is_individual": false
}
```

### C3 — GTM classifier
```
You are a talent-sourcing analyst.
Input: enriched profile data for a single person (JSON):
[paste EnrichmentData JSON here]

1. GTM function: Account Executive, SDR/BDR, Customer Success, Solutions Engineer, 
   RevOps, Marketing, Partnerships, Other.

2. Market segment they work: SMB, Mid-Market, Enterprise, Mixed.

3. Relevant (yes/no): relevant for [paste role description]?

4. Seniority: junior, mid, senior, lead, director, VP.

5. Company trajectory signal: did they join a company early (seed/A) and scale with it?
   strong / medium / weak / unknown.

Rules: base every judgment on evidence. Empty string if insufficient evidence.

Return JSON ONLY:
{
  "gtm_function": "",
  "market_segment": "",
  "relevant": "",
  "seniority": "",
  "trajectory_signal": ""
}
```

---

## EVALUATE PROMPTS

### EV1 — Level 2 evaluation (multi-signal)
```
You are evaluating a candidate profile for [role_title] at [company].

Role requirements:
[paste your intake rubric]

Target companies (Tier 1 — highest signal):
[list 8-10 target companies]

Candidate profile:
[paste enriched + classified JSON]

Score 0-100 across 4 dimensions:

1. Company signal (0-25)
   Currently at or recently left Tier 1 target company: 25
   At a strong adjacent company: 15
   At a relevant but lower-signal company: 8
   Not relevant: 0

2. Expertise depth (0-25)
   Strong public evidence (OSS, publications, talks, high-star repos): 25
   Some public evidence: 15
   No public evidence but strong company signal: 8
   No evidence: 0

3. Activity recency (0-25)
   Active last 30 days: 25
   Active last 90 days: 18
   Active last 6 months: 10
   Inactive over 6 months: 0

4. Community reach (0-25)
   500+ followers on most relevant platform: 25
   100-499: 15
   20-99: 8
   Under 20 or no presence: 0

Return JSON ONLY:
{
  "total_score": <0-100>,
  "tier": "<A|B|C|Pass>",
  "company_score": <0-25>,
  "expertise_score": <0-25>,
  "activity_score": <0-25>,
  "reach_score": <0-25>,
  "standout_signal": "<one specific thing worth highlighting in outreach>",
  "concern": "<one concern if any, empty string if none>",
  "recommended_action": "<outreach_now|add_to_pool|pass>"
}

Tier: A=75-100 (reach out now), B=50-74 (add to pool), C=25-49 (monitor), Pass=under 25
```

---

## CONTEXT PACK PROMPT

### CP1 — Full Context Pack builder
```
You are a senior talent strategist building a hiring Context Pack.

ROLE BRIEF:
[paste intake notes or JD here]

Build a complete Context Pack with these sections:

## REQUIREMENTS
Must-haves (non-negotiable):
Nice-to-haves (meaningful bonus):

## COMPENSATION
P25 / P50 / P75 for [role] at [level] in [location]:
Our stated range: [X] LPA
Assessment: [below/at/above market]
Source and date:

## MARKET
Supply: estimated qualified professionals in [location]
Estimated actively looking: (~15-20% of total)
Competition: 3-5 companies currently hiring this role
Hiring difficulty trend: [easier/harder vs. 6 months ago + reason]
Typical time to fill: [range in weeks]

## KEYWORDS
Primary titles: [all LinkedIn variations]
Skills: [15-20 relevant skills/tools]
Seniority synonyms: [all level descriptions]

## PERSONAS
Persona 1 — [archetype name]:
Background, where to find, what motivates them to move

Persona 2 — [archetype name]:
Background, where to find, what motivates them to move

## CHANNELS
Rank 5 channels from highest to lowest signal:
Channel, why high signal, specific access method

## TARGET COMPANIES
Tier 1 (source first): [5-8 companies + one sentence why]
Tier 2 (source after Tier 1): [5-8 companies]
Tier 3 (worth checking): [5-10 companies]

## TIMING
Best time to reach candidates: [month/quarter + reason]
Worst time: [month/quarter + reason]
Typical notice period: [range]
Time to start after offer: [total]

---
Version: 1.0 | Created: [date] | Role: [title] | Next review: [+4 weeks]
```

---

## CALIBRATION PROMPT

### CAL1 — Hiring Manager calibration document
```
Using this Context Pack: [paste Context Pack]

Generate a Hiring Manager calibration document:

1. CALIBRATION PROFILES (10 examples)
For each: Name or representative archetype, current title, company, 
one sentence on why they represent a strong match for this role.
Mix: 5 from Tier 1 target companies, 3 from adjacent companies, 
2 edge cases (unconventional backgrounds that could still work).

2. CALIBRATION QUESTIONS (3 questions to ask the HM)
Question that reveals which profile type they actually want.
Question that surfaces unstated preferences.
Question about which profiles are NOT right and why.

3. NOT THIS (3 false positives)
Profiles that look right on paper but are wrong, with explanation.

4. CLOSING QUESTION
"If I showed you the perfect candidate tomorrow, what would make you 
say yes in the first 5 minutes?"

Format: clean, readable, under 2 pages. This will be shared with the HM.
```

---

## OUTREACH PROMPTS

### O1 — Personalised outreach (single profile)
```
Write a personalised outreach message for this candidate.

Their profile: [paste enriched profile data]
Standout signal from evaluation: [paste standout_signal field]
Role: [role title] at [company]
The technical/business problem we are solving: [one sentence]

Rules:
- Under 80 words total
- First sentence: reference the specific standout signal — not their job title
- Second: one sentence on the problem we are solving
- Third: why their specific background is relevant (one phrase)
- Fourth: low-commitment ask
- No: "exciting opportunity", "rockstar", "passionate", "I hope this finds you well"
- Tone: peer-to-peer, not recruiter-to-candidate

Output: message only. No subject line. No preamble.
```

### O2 — Quarterly re-engagement (talent pool refresh)
```
Write a re-engagement message for a candidate in my talent pool.

About them: [name, title, company, why they were added to pool]
When we last spoke: [X months ago]
What has changed at our company since: [new funding / new project / team growth / etc.]
Role: [same role or updated role]

Write a message that:
- Acknowledges time has passed without being awkward
- Leads with what is new or different (not a copy of the first message)
- Is under 60 words
- Ends with a specific, low-commitment ask

Output: message only.
```

