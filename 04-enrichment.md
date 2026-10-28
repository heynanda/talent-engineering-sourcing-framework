# Step 2 — Enrichment

> "Find relevant online signals. Find all relevant signals on your candidate — contact info, social accounts, work history."
> "There are many service providers. LLM web search works well (but is expensive). Apollo, Clay, etc."

---

## What enrichment does

Takes a raw signal (a username, a name, a LinkedIn URL) and returns:
- Full name
- Personal website or portfolio URL
- LinkedIn URL
- Social profiles (Instagram, Dribbble, Behance, GitHub, X)
- Follower counts per platform
- Contact information

---

## Bence's enrichment prompt (shown in session)

This is the actual prompt Bence uses at ElevenLabs. It is built for LLM web search:

```
You are an OSINT research assistant.
Input: a single {token} that we KNOW belongs to the person of interest:
{url}? "{username / handle on that platform}": "{username}"; ""

This input is ground truth. Everything you return must describe THIS person.

Your task is enrichment only. Collect factual data points and do not 
evaluate, classify, rate or judge the person in any way.

1. Search the web and open the input profile to establish who this person is.
2. Find their full name.
3. Find their personal website / portfolio ({platform === "website" ? "Find it and return url": ""})
4. Find their profiles on Dribbble/Github (use the identity-matching rules below — a link that 
   belongs to a different person is worse than no link at all).
5. Find the follower count on each platform where you found a profile: X, LinkedIn, Instagram, 
   Dribbble and Behance. Search the profile pages and any third-party sources (social analytics sites, 
   archived pages, cached pages). Return the count. Return a single integer best-estimate per 
   platform (no commas, no ranges, no "k"/"m" suffix — e.g. 12500). Do NOT use the X/Twitter API.

IDENTITY MATCHING — this is the most important rule:
- Only return a profile link when you have positive evidence it is the SAME PERSON as {handle}.
- Acceptable evidence: the profile is linked from the input profile's bio, or from their personal 
  website or another already-confirmed profile; the profile links back to the input; the profile 
  shows the same full name AND matching context (same employer, same city, same conference bio, 
  award page); lists both profiles for the same person.
- A matching or similar username alone is NOT evidence. Neither is a common name alone.

If two or more different people plausibly own the profile, return an empty string.
Never construct or guess a URL to "fill in" a field. An empty string is the current answer 
whenever you are not confident.

Other rules:
- Return the "{platform === 'website' ? 'website' : '{platform}_url'}" field as the input 
  itself ({platform === 'website' ? '' : 'the URL of the profile'})
- Return every profile as a full URL, not a bare handle
- If unsure, return an empty string for that field
- Prefer LinkedIn over Crunchbase, GitHub, or other profiles
- If you don't find their personal website, a GitHub link is good as well
- Return their follower count as your best integer estimate from web search
- Only report a follower count for a platform whose profile link you actually returned
- Do not assess fit, seniority, role type, department, category, or whether the profile 
  is an individual vs. a company. Report only what you find.

Return JSON ONLY in this exact format:
{
  "name": "",
  "website": "",
  "x_url": "",
  "linkedin_url": "",
  "instagram_url": "",
  "dribbble_url": "",
  "behance_url": "",
  "x_followers": "",
  "linkedin_followers": "",
  "instagram_followers": "",
  "dribbble_followers": "",
  "behance_followers": ""
}
```

---

## Tool options for enrichment

| Tool | Best for | Cost | Speed |
|---|---|---|---|
| Claude with web search | Small batches, high accuracy | Medium per profile | Slow |
| Clay | Large batches, automated | Subscription | Fast |
| Apollo | GTM profiles (AE, SDR, CSM) | Subscription | Fast |
| Phantombuster | LinkedIn scraping at scale | Subscription | Medium |
| Hunter.io | Email finding | Per lookup | Fast |
| Proxycurl | LinkedIn profile enrichment via API | Per lookup | Fast |

---

## When to use which tool

**Use Claude with web search when:**
- You have 10–50 profiles to enrich
- Accuracy matters more than speed
- You need cross-platform social data (not just LinkedIn)
- Budget is limited

**Use Clay when:**
- You have 100+ profiles to enrich
- You need automation (run without touching it)
- You are enriching on a recurring cadence
- You need verified email addresses

**Use Apollo when:**
- Your profiles are primarily GTM (sales, marketing, CS)
- You need company data alongside personal data
- You want sequence management built in

---

## Data hygiene rules

1. **Never assume identity from username alone.** If you cannot confirm it is the same person with positive evidence, leave the field blank.
2. **Empty string over wrong data.** A blank field is infinitely better than a URL pointing to a different person.
3. **Follower counts are estimates.** Label them as such in your sheet. They are signals, not facts.
4. **Re-enrich every 6 months.** People change companies, delete accounts, and grow audiences. Stale data produces bad outreach.

