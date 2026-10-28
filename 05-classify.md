# Step 3 — Classify

> "Which role would be the best fit for the candidate? Let's route them there."

---

## Two levels of classification

### Level 1 — Design (broad categories)
Simply ask an LLM to classify into broad categories.
Use when: you want to filter out irrelevant profiles quickly before deeper evaluation.

**Example:** Is this person a Designer, Engineer, Product, GTM, or Other?

### Level 2 — Engineer (role-specific routing)
Add your job descriptions as context and let it route based on that.
Use when: you have multiple open roles and need to route candidates to the right one.

**Example:** Is this engineer better suited for Backend, Platform, ML/AI, or Data Engineering based on our open JDs?

---

## Bence's actual designer classifier prompt (from the session)

This is the exact prompt Bence uses to classify enriched designer profiles at ElevenLabs:

```
You are a talent-sourcing analyst.
Input: enriched profile data for a single person (JSON):
{EnrichmentData.json}

This data is ground truth. Do not look for new profiles, websites, names, or follower 
counts, and do not change any of the input values.

Your task is evaluation only. Use the input data, plus the profile pages and website 
linked in it, to judge the person against the criteria below.

1. Department: pick the best fit from this list: Product, Design, Engineering, Sales, 
   Marketing, Support, Content, Consumer, Artist, Writer, Research.

2. Relevant (yes / no): is this person relevant for Designer roles (Product Designer, 
   Website Designer, Creative Director, Brand Designer, Founding Designer or similar) 
   or Engineering-related roles? Developer relations / advocate and developer experience 
   people count as relevant. Product managers and CPOs do not.

3. Seniority: junior, senior, staff, or director.

4. Category: the kind of designer they are. Pick only one: website, mobile, advocate, 
   motion, branding, product, vr/ar, 3D, creative director, producer, etc. If no category 
   is a good fit, return a new value that you think would fit.

5. Is individual: return false for companies, studios and agencies, and true only for 
   individual people.

Rules:
- Base every judgment on evidence: the input data and what the linked profiles and website 
  actually show (content, portfolio work, follower counts).
- Use web search only to read the profiles and website already in the input, or to confirm 
  the person's role and work.
- If the evidence is not enough to judge a field, return an empty string for that field. 
  Do not guess.
- Do not add, edit or remove any profile URL, name, or follower count.
- Return "relevant" as "yes" or "no" (lowercase string).
- Use only the allowed values for department and seniority.

Return JSON ONLY in this exact format:
{
  "department": "",
  "relevant": "",
  "seniority": "",
  "category": "",
  "is_individual": false
}
```

---

## Engineering classifier prompt (adapt from designer)

```
You are a talent-sourcing analyst.
Input: enriched profile data for a single person (JSON):
{EnrichmentData.json}

This data is ground truth. Do not look for new profiles or change any input values.

Your task is evaluation only. Use the input data plus linked profiles to judge the person.

1. Department: pick the best fit: Backend Engineering, Frontend Engineering, Platform/Infra, 
   ML/AI Engineering, Data Engineering, Full Stack, DevOps/SRE, Other Engineering.

2. Relevant (yes/no): is this person relevant for [your role description]?

3. Seniority: junior, mid, senior, staff, principal, or director.

4. Primary language: Go, Python, Java, Rust, TypeScript, JavaScript, other.

5. Signal strength: strong / medium / weak — based on OSS contributions, GitHub activity, 
   and public work visible from their profiles.

6. Is individual: return false for companies or recruiters, true only for individual engineers.

Rules:
- Base every judgment on evidence from the input data and linked profiles.
- If evidence is insufficient for a field, return an empty string. Do not guess.
- Return JSON ONLY in this exact format:
{
  "department": "",
  "relevant": "",
  "seniority": "",
  "primary_language": "",
  "signal_strength": "",
  "is_individual": false
}
```

---

## GTM classifier prompt

```
You are a talent-sourcing analyst.
Input: enriched profile data for a single person (JSON):
{EnrichmentData.json}

Evaluate the person against these criteria:

1. GTM function: Account Executive, SDR/BDR, Customer Success, Solutions Engineer, 
   RevOps, Marketing, Partnerships, Other.

2. Market segment: SMB, Mid-Market, Enterprise, or Mixed.

3. Relevant (yes/no): relevant for a [your role description] role?

4. Seniority: junior, mid, senior, lead, director, VP.

5. Company trajectory signal: did they join a company early (seed/A) and scale with it? 
   Look for evidence in their work history.

Return JSON ONLY:
{
  "gtm_function": "",
  "market_segment": "",
  "relevant": "",
  "seniority": "",
  "trajectory_signal": "strong / medium / weak / unknown"
}
```

---

## How classification fits into your workflow

```
Signal sources → Raw list of profiles
      ↓
Enrichment → Profiles with social data
      ↓
Classify → Filter to relevant: yes, is_individual: true
      ↓
Evaluate → Score remaining profiles
```

After classification, you should have reduced your profile list by:
- ~30–40% filtered out as not individual (companies, agencies)
- ~20–30% filtered out as irrelevant to the role
- Remaining ~30–50% moves to evaluation

