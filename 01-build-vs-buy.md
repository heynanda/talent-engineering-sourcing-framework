# Build vs Buy — When to Build Automations

> From Bence Gedai's session: "Building automations take time, and we're already busy."
> In most other cases the ROI doesn't make sense. With your existing stack (LinkedIn Recruiter, Juicebox, Gem) you can most likely get decent coverage and a head start.

---

## When TO build

### 1. Niche role or high talent bar
Roles where you want good coverage of the target talent pool, or where the go-to searches run out of candidates.

**Examples:**
- Staff+ engineers in a very specific domain (e.g. distributed systems + Go + Bangalore)
- Motion designers with VR/AR experience
- AI researchers with specific model architecture experience

**Signal that you need automation:** You have run every LinkedIn search variation and Juicebox query. The pool is exhausted. You need to go where other recruiters are not looking.

### 2. Volume hiring
If you have 5+ of the same or similar role, it makes sense to invest in automations.

**Examples:**
- 10 software engineers across 3 months
- 20 BDRs for a GTM expansion
- 15 designers for a product scaling push

**Signal that you need automation:** You are running the same sourcing search repeatedly. The ROI of building it once and running it 10 times is clear.

### 3. Lower competition
If we do it right, we'll find hidden gems — candidates who don't get approached by all your competitors.

**Examples:**
- GitHub contributor lists (competitors are on LinkedIn, not GitHub)
- Newsletter subscriber scrapes (award winners, podcast guests)
- Community members in niche Slack groups

**Signal that you need automation:** The obvious places are saturated. Response rates on LinkedIn InMail are below 15%.

---

## When NOT to build

- You have 1–2 open roles with standard profiles
- Your existing stack (LinkedIn Recruiter, Juicebox, Gem) covers the search
- The role is generalist and the pool is large
- You are earlier than 2 weeks into a search — exhaust conventional methods first

---

## Decision rule

```
Is the pool large enough on LinkedIn/Juicebox? 
  YES → Use existing tools. Do not build.
  NO → Is this role recurring or 5+ headcount?
        YES → Build the automation. ROI is justified.
        NO → Is this a niche role where competitors are NOT looking?
              YES → Build the automation. Unfair advantage.
              NO → Use existing tools. Not worth the build time.
```

---

## Time investment reality check

| Automation type | Build time | Ongoing maintenance | ROI threshold |
|---|---|---|---|
| GitHub contributor scraper | 2–4 hours | Low | 3+ technical roles |
| Newsletter/award list scraper | 1–3 hours | Low | 2+ niche roles |
| LLM enrichment pipeline | 4–8 hours | Medium | 5+ roles of same type |
| Full classify + evaluate pipeline | 8–16 hours | High | 10+ roles, recurring |

