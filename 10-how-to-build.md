# How to Build — 8 Principles

> "Automations can help you scale, but we still need Talent / Human In The Loop to identify the right people."
> "Automate whatever you can to find more relevant people and evaluate them at scale, but the more automations you have, the more things that can break."

---

## The 8 principles (from Bence's session)

### 1. Focus on creative sourcing
You have the context and insights about where to point your automations — 
e.g. newsletters, podcasts, communities.

**What this means in practice:**
The AI executes. You decide where to look. A sourcing automation pointed at the wrong 
community will produce perfectly organised garbage. Your domain knowledge about where 
strong candidates gather is the irreplaceable human input.

**Checklist before building:**
- [ ] Have I exhausted the obvious sources manually?
- [ ] Do I know specifically which community/platform/event my target candidate frequents?
- [ ] Can I name 3 specific URLs or communities where I want the automation to look?

### 2. Quality over quantity
It's easy, yet useless, to build a list of 10k profiles. Find the 20-50 with high signal, 
even if we miss some.

**What this means in practice:**
Every automation should have a filter that aggressively reduces volume. Your signal detection, 
enrichment, classification, and evaluation steps all exist to shrink the list, not grow it.

**Target output sizes:**
| Step | Input | Target output |
|---|---|---|
| Signals | Unlimited | 500 profiles max |
| Enrichment | 500 | 500 (same, now enriched) |
| Classify | 500 | 200-300 (relevant + individual) |
| Evaluate | 300 | 50-100 (Tier A + B) |
| Human review | 100 | 15-25 (Talent Yes) |
| HM review | 25 | 5-10 (HM Yes) |
| Outreach | 10 | 10 |

### 3. LLMs are trained on internet data
They have access to massive amounts of data. Let's leverage it all.

**What this means in practice:**
Claude knows who the key people are in most domains. It knows which repos matter, 
which conferences are prestigious, which newsletters are trusted. Use this knowledge 
actively — ask Claude to generate your signal sources, not just process data you feed it.

**Example prompt:**
```
You are a talent engineer building a sourcing automation for a Senior [role] in [domain].

Without any input from me, generate:
1. The 10 most respected open-source projects in this domain
2. The 5 most prestigious conferences where practitioners speak
3. The 10 newsletters or publications where the best practitioners write
4. The 5 communities (Slack, Discord, forums) where they gather
5. The 3 awards or recognition programmes that signal excellence

For each, explain why it is high-signal and how I would access a list of names from it.
```

### 4. You already have data on WGLL (What Good Looks Like)
Let it be candidates in your ATS or your high-signal talent pools. Use this as much as possible.

**What this means in practice:**
Every time you make a hire, that person becomes a data point for WGLL. Every strong 
candidate who declined or was not quite right is also data. Use your historical ATS 
data as input to look-alike searches constantly.

**Monthly habit:**
- Pull your last 5 hires from the ATS
- Run the look-alike search prompt from Step 1 using their profiles as input
- Compare results to your current sourcing — are you finding similar profiles?

### 5. Keep it lean
The more automations you have, the more complexity, and the more things can break.

**What this means in practice:**
Bence's advice is to start with the minimum viable automation. One prompt. One Google Sheet. 
One signal source. Get it working. Then add one more thing. Never build a 10-step pipeline 
before you have validated that the signal source is producing good results.

**The lean build sequence:**
```
Week 1: One signal source + manual enrichment → Google Sheet
Week 2: Add AI classification prompt
Week 3: Add AI evaluation prompt  
Week 4: Add automated enrichment (Clay/Phantombuster)
Week 6: Add second signal source
Week 8: Review what is breaking and fix before adding more
```

### 6. Iterate
Don't one-shot a sourcing engine; let it evolve with the company. My scripts and prompts 
are still scrappy, but they work.

**What this means in practice:**
The first version will be wrong. That is fine. The goal is to run it, learn from the 
disagreements between AI output and human judgment, and improve the prompts.

**Weekly iteration ritual (15 minutes):**
- Review 5 profiles where AI said A and you said No — why?
- Review 5 profiles where AI said C and you said Yes — why?
- Update one thing in the evaluation prompt based on what you learned
- Note the date and change in a "prompt changelog" section of your sheet

### 7. One source of truth
Gather all your sourced candidates in one place to avoid duplicates.

**What this means in practice:**
One Google Sheet per role. All signal sources feed into the same sheet. 
Before adding any new profile, check if they are already there (use VLOOKUP or 
Ctrl+F on their LinkedIn URL as the unique identifier).

**The unique identifier rule:**
LinkedIn URL is your primary key. Every profile in every sheet is identified 
first by their LinkedIn URL. Never use name as the unique identifier — too many 
people have the same name.

**Deduplication across roles:**
Maintain a master talent pool sheet that spans all roles. When someone appears 
in two role-specific sheets, note it — they may be right for either role depending 
on what opens.

### 8. Build for yourself first
Enabling your whole team is a whole different game with topics like compliance, 
security, scalability.

**What this means in practice:**
Build for your own workflow first. Make sure it produces good results for you before 
worrying about whether it scales to your whole team or org. The biggest mistake is 
building team infrastructure before validating the approach works at all.

**The maturity ladder:**
```
Stage 1: You use it yourself. Scrappy. Works.
Stage 2: One colleague uses it. Document the steps.
Stage 3: Small team uses it. Clean up the prompts. Add a README.
Stage 4: Whole team uses it. Add error handling. Consider compliance. Think about security.
```

Most solo recruiters never need to go past Stage 2. That is fine.

---

## Common mistakes and how to avoid them

| Mistake | Why it happens | Fix |
|---|---|---|
| Building before validating the signal source | Excitement about automation | Run 20 profiles manually first. Only automate what produces good manual results. |
| Using LLMs to generate outreach at scale | Wanting to save time on messaging | The hard work (finding the right person) is what gets replies. Save human time there instead. |
| Building a 10-step pipeline before testing step 1 | Engineering mindset | Validate each step independently before connecting them. |
| Never updating the evaluation prompt | Set-and-forget mentality | Weekly 15-minute calibration review. Non-negotiable. |
| Sharing unreviewed AI output with the HM | Trusting AI too much | Human review (Step 5) is mandatory before anything reaches the HM. Always. |
| Not logging why profiles were rejected | Moving too fast | The rejection reasons are your most valuable training data. Always capture them. |

