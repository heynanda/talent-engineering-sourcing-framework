# Bryan Hong's Talent One — Context Pack System

> From Bryan Hong, Chief Systems Officer at Wizard.
> "Eleven agents, one shape. Ask for one document or all eight. Nothing waits that doesn't have to."

---

## What Talent One is

Talent One is Bryan Hong's agentic recruiting system at Wizard. It takes a single role brief 
as input and uses 11 AI agents working in parallel to produce a complete hiring package — 
calibration document, JD, sourcing playbook, outreach campaign, interview plan, and more.

The core insight: **One file every document trusts. Researched once per role. Every specialist 
reads the same facts.**

---

## The Execution Graph

```
INPUT                    RELAY + SCOUT              SHARED              SPECIALIST AGENTS
Role brief     →     Plans the run    →     Context Pack     →     HM calibration
               →     Researches       →     (versioned)      →     Role education
                                                             →     Talent map
                                                             →     Job description
                                                             →     Sourcing playbook
                                                             →     Outreach campaign
                                                             →     Interview plan
                                                             →     Recruiter screen

                                            RENDER → Verify → QA GATE → Certify
```

**How it works:**
1. You input a role brief (or your own JD)
2. RELAY agent plans the run — decides which documents are needed
3. SCOUT agent researches the role, market, and company context
4. Both feed into a shared CONTEXT PACK — one source of truth
5. Eight specialist agents read the same Context Pack and produce their outputs in parallel
6. RENDER agent verifies all outputs
7. QA GATE certifies before anything ships

**Key principle:** Nothing waits that does not have to. Agents run in parallel where possible.

---

## The Context Pack — the most important concept

> "One file every document trusts. Researched once per role. Every specialist reads the same facts."

The Context Pack is a versioned document that contains everything any agent (or human) 
needs to know about this role. It is built once at the start of each hiring run and 
updated as conditions change.

### What goes into a Context Pack

**Inputs (left side):**

| Section | What it contains |
|---|---|
| Requirements | Must-haves, nice-to-haves — the non-negotiables and the preferences |
| Compensation | One canonical range — no ambiguity, no "it depends" |
| Market | Supply, demand, competitors — how many people exist, who else is hiring them |
| Keywords | Titles, synonyms, skills — every way this role might be described |

**Outputs (right side — what agents use Context Pack to produce):**

| Output | What it is |
|---|---|
| Personas | Who you're looking for — 2-3 specific profiles of ideal candidates |
| Channels | Where they actually are — specific platforms, communities, repos |
| Targets | Companies worth sourcing from — the shortlist of target employers |
| Timing | When people tend to move — seasonality, budget cycles, layoff patterns |

**The grounded data rule:** Every number carries a source, a method, and a date. 
Estimates stay labelled as estimates.

---

## How to build your own Context Pack (without the full agent system)

You do not need 11 agents to use this concept. Here is a simple version you can build 
with Claude today:

### Context Pack prompt

```
You are a senior talent strategist. I am about to start hiring for this role:

ROLE BRIEF:
[paste your intake notes or JD here]

Build me a Context Pack for this role with these exact sections:

## REQUIREMENTS
Must-haves (dealbreakers if missing):
- [list]

Nice-to-haves (meaningful bonus, not required):
- [list]

## COMPENSATION
Based on market data for [role] at [level] in [location] at a [stage] company:
- P25: [range] LPA
- P50: [range] LPA  
- P75: [range] LPA
- Our stated range: [X] LPA
- Assessment: [below market / at market / above market]
- Source: Levels.fyi, LinkedIn Salary, Glassdoor India (estimated, as of [date])

## MARKET
Supply:
- Estimated number of qualified professionals in [location]: [number, source]
- How many are likely actively looking: [estimate, ~15-20% of total]
- Competition: [list 3-5 other companies currently hiring this role]

Demand:
- Is this role getting harder or easier to fill vs. 6 months ago? [assessment + reason]
- Typical time to fill at similar companies: [range in weeks]

## KEYWORDS
Primary titles: [list all ways this role is described on LinkedIn]
Skills keywords: [list 15-20 relevant skills/tools]
Seniority synonyms: [all the ways the level is described]

## PERSONAS
Persona 1 — [name this archetype]:
- Background: [2 sentences]
- Where to find them: [specific sources]
- What motivates them to move: [1-2 factors]

Persona 2 — [name this archetype]:
- Background: [2 sentences]
- Where to find them: [specific sources]
- What motivates them to move: [1-2 factors]

## CHANNELS
Rank these from highest to lowest signal for this role:
1. [Channel] — why: [reason] — how to access: [specific action]
2. [Channel] — why: [reason] — how to access: [specific action]
3. [Channel] — why: [reason] — how to access: [specific action]
4. [Channel] — why: [reason] — how to access: [specific action]
5. [Channel] — why: [reason] — how to access: [specific action]

## TARGET COMPANIES
Tier 1 (highest signal, source from here first):
[list 5-8 companies with one sentence on why each is Tier 1]

Tier 2 (strong signal, source after Tier 1 exhausted):
[list 5-8 companies]

Tier 3 (worth checking, lower priority):
[list 5-10 companies]

## TIMING
Best time to reach candidates: [month/quarter and why]
Worst time to reach: [month/quarter and why]
Typical notice period for this role: [range]
Estimated time to start after offer: [total timeline]

---
Context Pack version: 1.0
Created: [date]
Role: [title]
Next review: [date + 4 weeks]
```

---

## The eight documents Talent One produces

For each of these, a specialist agent reads the Context Pack and produces the document.
You can replicate each with a focused Claude prompt using your Context Pack as input.

### 1. HM Calibration document
**What it is:** A calibration list + discussion guide for the hiring manager conversation.
**Includes:** 10-15 real profiles representing different interpretations of the role, 
3 calibration questions to ask the HM, and a "not this" section showing profiles that 
look similar but are wrong.

**Prompt:**
```
Using this Context Pack: [paste Context Pack]

Generate a Hiring Manager calibration document with:
1. 10 real or representative profiles (name, title, company, one sentence on why they 
   represent a strong match) — pull from LinkedIn or generate representative examples
2. 3 calibration questions that will reveal the HM's unstated preferences
3. A "not this" section: 3 profiles that look right on paper but are wrong, 
   with an explanation of why each is a false positive
4. One question to ask at the end: "If I showed you the perfect candidate tomorrow, 
   what would make you say yes in the first 5 minutes?"
```

### 2. Role education
**What it is:** A brief that educates the recruiter on the domain before sourcing begins.
**Includes:** What this type of engineer/designer/PM actually does day-to-day, 
the tools they use, how they think, what they care about.

**Prompt:**
```
Using this Context Pack: [paste Context Pack]

Write a role education brief for a recruiter who has never hired a [role] before.
Include:
1. What this person does on a typical day (specific, not generic)
2. The 5 tools/technologies they use most — what each one does in plain English
3. How they evaluate a new opportunity (what makes them say yes, what makes them say no)
4. The 3 most common misconceptions recruiters have about this role
5. 5 questions to ask in a recruiter screen that will quickly reveal if someone is 
   genuinely strong vs. inflating their experience
```

### 3. Talent map
**What it is:** A visual or structured map of where talent is concentrated.
**Includes:** Company clusters, geography, community hubs, and career paths.

### 4. Job description
**What it is:** A complete, candidate-facing JD written from the Context Pack.
**Includes:** Role overview, what you will do, what we are looking for, what we offer.

### 5. Sourcing playbook
**What it is:** A step-by-step sourcing plan specific to this role and moment.
**Includes:** Which channels to work in which order, specific search strings, 
target company list, signal sources to activate.

### 6. Outreach campaign
**What it is:** Message templates personalised to each persona from the Context Pack.
**Includes:** 3 variations of the opening message (one per persona), follow-up sequence, 
re-engagement message.

### 7. Interview plan
**What it is:** The complete interview structure for this role.
**Includes:** Number of rounds, who interviews in each, what each round evaluates, 
sample questions per round, scorecard template.

### 8. Recruiter screen guide
**What it is:** A script and evaluation framework for the recruiter's first call.
**Includes:** Opening, 5 qualifying questions, red flag checklist, 
what to say about the role, how to close for next steps.

---

## How to use this system today (without agents)

You do not need to build all 11 agents. Here is the minimum viable version:

**Week 1:** Build the Context Pack prompt. Run it for every new role before you start sourcing.

**Week 2:** Add the HM Calibration document. Share before any sourcing conversation.

**Week 3:** Add the Sourcing Playbook output. Replace your ad-hoc sourcing with a plan.

**Week 4:** Add the Outreach Campaign. Three persona-specific message templates.

**Month 2:** Add the Recruiter Screen Guide. Consistent first-call quality.

**Month 3:** Add the Interview Plan. Consistent evaluation quality.

The Context Pack is the foundation. Everything else is built on it. Start there.

