# Search Queries for Job Scraper

<!-- Configured for Adam Soliman on 2026-07-31. -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` uses the single `.agents/skills/search-jobs/SKILL.md` entry point. That skill discovers every enabled source adapter under `.agents/skills/search-jobs/sources/*/SOURCE.md` and runs its CLI first. Shipped country-agnostic adapters include `linkedin-search` and `freehire-search`; Danish demos and adapters added with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

## Search Sites

Primary:
- **linkedin.com/jobs** - LinkedIn job listings, filtered first for New York and then the Northeast, San Francisco, and other U.S. locations; also covered by `linkedin-search` CLI
- **freehire.me** - multi-market technical job aggregator, covered by `freehire-search` CLI
- **[SimplifyJobs New-Grad Positions](https://github.com/SimplifyJobs/New-Grad-Positions)** - check the README's **Software Engineering** and **Data Science, AI & Machine Learning** sections on every search. Include only open roles matching the configured location preferences; follow the direct employer application link and verify it is still active before presenting a role.
- **Company career pages and public ATS boards** - check the target-company list below directly on every search; do not wait for an aggregator to index a new posting

### Direct target-company sweep (required every run)

Check the official career site or public ATS board for each company below. Use the
company site's own search when available; otherwise query its Greenhouse, Lever,
Ashby, Workday, or other official ATS board. Search the full role-title matrix in
this file, not only titles containing `new grad` or a graduation year.

- Priority targets: Google, Notion, Stripe, Databricks, Snowflake
- Major technology companies: Lyft, Uber, Airbnb, Meta, Microsoft, Amazon, Apple,
  NVIDIA, TikTok, Bloomberg, Palantir
- High-growth technology companies: Anthropic, OpenAI, Scale AI, Datadog, Ramp,
  Rippling, Coinbase, Block, DoorDash, Roblox, Samsara, Cloudflare, Figma

Treat the official employer posting as authoritative. Record when a company site
was checked even if it returned no matching roles. An empty aggregator result does
not replace this direct sweep.

### Entry-level title and description signals

Search for all of these title families:

- Software Engineer, Software Engineer I, Software Engineer 1, Associate Software
  Engineer, Junior Software Engineer
- Data Scientist, Data Scientist I, Data Scientist 1, Associate Data Scientist,
  Junior Data Scientist
- Data Engineer, Data Engineer I, Data Engineer 1, Associate Data Engineer, Junior
  Data Engineer
- Machine Learning Engineer, Machine Learning Engineer I/1, Associate or Junior
  Machine Learning Engineer
- AI Engineer, AI Engineer I/1, Associate or Junior AI Engineer

Also consider a plain title such as `Software Engineer`, `Data Scientist`, or `Data
Engineer` when the description contains an entry-level signal: `associate`,
`entry-level`, `early career`, `new grad`, `new graduate`, `recent graduate`,
`university graduate`, `campus`, `0-2 years`, or `1+ years`. Do not require `2027`
or `new grad` to appear in the title. Exclude clearly senior roles and titles marked
II/2 or higher unless the description explicitly identifies them as entry-level.

## Query Categories

Queries are grouped by priority. Each query should be combined with your location terms (e.g. your city, region, or metro area) where the site supports it.

### Priority 1: New-Grad Software Engineering

These match your strongest and most desired career direction.

```
site:linkedin.com/jobs "new grad software engineer" "New York"
site:linkedin.com/jobs "software engineer" "university graduate" "New York"
site:linkedin.com/jobs ("Software Engineer I" OR "Software Engineer 1" OR "Associate Software Engineer" OR "Junior Software Engineer") "United States"
site:boards.greenhouse.io OR site:jobs.ashbyhq.com OR site:jobs.lever.co ("Software Engineer I" OR "Software Engineer 1" OR "Associate Software Engineer" OR "Junior Software Engineer")
site:boards.greenhouse.io OR site:jobs.ashbyhq.com OR site:jobs.lever.co "Software Engineer" ("entry-level" OR "early career" OR "0-2 years" OR "1+ years")
site:careers.google.com "software engineer" "university graduate"
```

### Priority 2: New-Grad AI / Machine Learning Engineering

These match your domain expertise.

```
site:linkedin.com/jobs "machine learning engineer" "new grad" "New York"
site:linkedin.com/jobs "AI engineer" "new grad" "United States"
site:linkedin.com/jobs ("Machine Learning Engineer I" OR "Associate Machine Learning Engineer" OR "AI Engineer I" OR "Associate AI Engineer") "United States"
site:jobs.lever.co OR site:boards.greenhouse.io "machine learning engineer" "university" "New York"
site:jobs.lever.co OR site:boards.greenhouse.io OR site:jobs.ashbyhq.com ("Machine Learning Engineer I" OR "Associate Machine Learning Engineer" OR "AI Engineer I" OR "Associate AI Engineer")
```

### Priority 3: Data / AI Platform Engineering

Adjacent roles you could pivot into.

```
site:linkedin.com/jobs "data engineer" "new grad" "New York"
site:linkedin.com/jobs ("Data Engineer I" OR "Data Engineer 1" OR "Associate Data Engineer" OR "Junior Data Engineer") "United States"
site:linkedin.com/jobs ("Data Scientist I" OR "Data Scientist 1" OR "Associate Data Scientist" OR "Junior Data Scientist") "United States"
site:boards.greenhouse.io OR site:jobs.ashbyhq.com OR site:jobs.lever.co ("Data Engineer I" OR "Associate Data Engineer" OR "Data Scientist I" OR "Associate Data Scientist")
site:boards.greenhouse.io OR site:jobs.ashbyhq.com OR site:jobs.lever.co ("Data Engineer" OR "Data Scientist") ("entry-level" OR "early career" OR "0-2 years" OR "1+ years")
site:linkedin.com/jobs "software engineer" "AI platform" "New York"
site:careers.databricks.com OR site:careers.snowflake.com "university" engineer
```

### Priority 4: Broader Technical / Consulting

Wider net for general technical roles.

```
site:linkedin.com/jobs "software engineer intern" "Spring 2027" "New York"
site:linkedin.com/jobs "machine learning intern" "Spring 2027" "United States"
site:jobs.ashbyhq.com OR site:jobs.lever.co "software engineer intern" "Spring 2027"
```

## Location Filter

When evaluating results, verify the job location is within reasonable commute distance from your home. Define acceptable areas:
- New York City and the surrounding metropolitan area (ideal)
- Northeast U.S. (acceptable)
- San Francisco Bay Area (acceptable for a strong role)
- Other U.S. locations (consider case by case)
- International locations (not configured; discuss before including)

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- "/scrape [focus_area]" -> relevant category queries + custom focus-specific queries
