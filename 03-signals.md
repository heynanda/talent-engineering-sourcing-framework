# Step 1 — Signals

> "The more high-signal data you have on WGLL (what good looks like), the easier your job gets. Lean on your team and Claude to get creative sourcing ideas."

---

## The 4 signal types

### 1. Lookalike search
You have a list of people or companies already identified as high potential. Find me similar ones.

**How to use:**
- Take your top 5 candidates from previous hires or your talent pool
- Give Claude the list and ask it to identify patterns
- Use those patterns to search for more like them

**Example prompt:**
```
I have these 5 people who were strong candidates for our [role]:
[paste profiles or descriptions]

What do they have in common in terms of:
- Career trajectory
- Companies they worked at
- Communities they participate in
- Content they create or share
- Skills and tools they use

Based on these patterns, suggest 10 specific places I should look for more people like them.
```

### 2. Network discovery
"Great people know other great people" — map out their networks and look for intersections.

**How to use:**
- Find 3 strong profiles you already have
- Ask Claude to identify their likely LinkedIn connections, followers, collaborators
- Look for people who appear in multiple networks (high-signal intersection)

**Example prompt:**
```
These 3 people are strong signals for the type of [designer/engineer/PM] I am looking for:
[paste profiles]

If I were to map their professional networks, where would they likely intersect?
What conferences do they all attend? What communities are they in? 
What newsletters or podcasts do they follow or contribute to?
Give me 5 specific places to look for people at the intersection of their networks.
```

### 3. Social engagement
Follower base, comments, reshares, interactions on social platforms.

**How to use:**
- Find the most-followed people in your target domain
- Look at who actively engages with their content (not just follows)
- Active engagers are more likely to be practitioners than lurkers

**Example prompt:**
```
I am sourcing [role type]. 

These are the top voices in this space whose audience would contain my target candidates:
[list 3-5 relevant accounts]

What types of content do these people post that gets the most engagement from practitioners 
(not just fans)? What does an engaged comment from a strong candidate look like vs. a casual follower?
```

### 4. Expert recognition
Awards, conferences, articles, podcasts, newsletters, credits, etc.

**How to use:**
- Find industry award lists, conference speaker rosters, newsletter contributors
- These people have been publicly validated by their peers
- Their public recognition is a proxy for quality

**Example prompt:**
```
I am hiring a [role] in [domain].

Give me a list of 10 specific:
- Awards or recognition programmes in this space
- Conferences where speakers represent the calibre I am looking for
- Newsletters or publications where contributors/authors would be strong candidates
- Podcasts where guests represent the expertise level I need

For each, explain what makes it a high-signal source and how I would access the list of names.
```

---

## Bence's actual signal prompts (from the session)

### Prompt 1 — Generate sourcing ideas
```
You're a talent engineer. Do a deep research, build me a comprehensive list 
of ideas to gather signals online for strong [designers/engineers/PMs], 
e.g. awards, jury member, podcast speakers, etc. Be very specific about 
platform types and concrete platforms. Gather your findings in a table: 
type, concrete sources, signal strength prediction, implementation difficulty to automate.
```

### Prompt 2 — Pull list of credited people from agency/company website
```
Check [agency website] studio, search online, go through website references, 
go through website references, look at their case studies to build a comprehensive 
list of all the [video editors / designers / engineers] who currently or in the 
past worked there.

For each of these people, do a separate web search, find me their name, job title, 
location country, LinkedIn url, portfolio website url, social media urls. Make sure 
to only link urls if you're certain they belong to the same person.

Write your outputs to a tsv format.
```

### Prompt 3 — Pull list of agencies and speakers from newsletter
```
Review the first 5 pages at: [target newsletter URL]

Review all the agencies and individuals on these newsletter listings, as an output, 
give me a tsv for all the agencies and another tsv for all the individuals.

For individuals try to find their LinkedIn page, website and social links 
(Instagram, X, Dribbble, Behance, etc.) — highlight the one where they're most active, 
that could be their portfolio work; also find their job title and location.

For agencies, return me the agency name, location, predicted size, their LinkedIn url, 
website url and relevant social links.
```

### Prompt 4 — Look-alike search based on your Talent Pool
```
Do a deep research based on profiles we already identified as high targets, 
find me similar people, return them in a tsv format.

Input: [copy your talent pool — paste the names, titles, companies of your top profiles]
```

---

## Signal sources by role type

### Engineering
| Source | Signal type | How to access |
|---|---|---|
| GitHub contributor lists | Expert recognition | github.com/[repo]/graphs/contributors |
| OSS Signal Radar | Expert recognition | oss-signal-radar.lovable.app |
| Conference speaker lists (KubeCon, PyCon, ReactConf) | Expert recognition | Manual scrape or LLM prompt |
| Stack Overflow top contributors | Expert recognition | stackoverflow.com/users?tab=reputation |
| Technical blog authors | Expert recognition | LLM web search prompt |

### Design
| Source | Signal type | How to access |
|---|---|---|
| Awwwards jury members | Expert recognition | awwwards.com/jury |
| Dribbble most followed | Social engagement | dribbble.com/designers |
| Figma Community plugin authors | Lookalike / Expert | figma.com/community |
| Read.cv profiles | Expert recognition | read.cv/explore |
| Design conference speakers (Config, SXSW Design) | Expert recognition | Conference websites |

### Product
| Source | Signal type | How to access |
|---|---|---|
| Lenny's Newsletter contributors | Expert recognition | lennysnewsletter.com |
| ProductHunt makers | Expert recognition | producthunt.com/makers |
| Substack top PM writers | Expert recognition | LLM web search prompt |
| Mind the Product speakers | Expert recognition | mindtheproduct.com |

### GTM
| Source | Signal type | How to access |
|---|---|---|
| SaaStr speaker list | Expert recognition | saastr.com/speakers |
| RevGenius top contributors | Social engagement | Community observation |
| G2 reviewer profiles | Expert recognition | g2.com |
| Apollo search by company trajectory | Lookalike | Apollo enrichment |

