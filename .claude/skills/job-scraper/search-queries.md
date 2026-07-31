# Search Queries for Job Scraper

<!-- Configured for Adam Soliman on 2026-07-31. -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

## Search Sites

Primary:
- **linkedin.com/jobs** - LinkedIn job listings, filtered first for New York and then the Northeast, San Francisco, and other U.S. locations; also covered by `linkedin-search` CLI
- **freehire.me** - multi-market technical job aggregator, covered by `freehire-search` CLI
- **Company career pages** - especially Google, Notion, Stripe, Databricks, and Snowflake

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

Queries are grouped by priority. Each query should be combined with your location terms (e.g. your city, region, or metro area) where the site supports it.

### Priority 1: New-Grad Software Engineering

These match your strongest and most desired career direction.

```
site:linkedin.com/jobs "new grad software engineer" "New York"
site:linkedin.com/jobs "software engineer" "university graduate" "New York"
site:careers.google.com "software engineer" "university graduate"
```

### Priority 2: New-Grad AI / Machine Learning Engineering

These match your domain expertise.

```
site:linkedin.com/jobs "machine learning engineer" "new grad" "New York"
site:linkedin.com/jobs "AI engineer" "new grad" "United States"
site:jobs.lever.co OR site:boards.greenhouse.io "machine learning engineer" "university" "New York"
```

### Priority 3: Data / AI Platform Engineering

Adjacent roles you could pivot into.

```
site:linkedin.com/jobs "data engineer" "new grad" "New York"
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
