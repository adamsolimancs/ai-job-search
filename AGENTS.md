---
framework_version: 1.0.0
---

# Agent Guidelines: AI Job Search

This workspace is structured to manage job search activities, scraper tools, CVs, cover letters, and interview preparation.

## Thin-Pointer Design (Single Source of Truth)

To prevent duplication and configuration drift across different AI agent frameworks (Claude Code, Google Antigravity, Codex, Cursor, Gemini CLI, etc.), this workspace uses a unified thin-pointer design. All agent runtimes should load the canonical specifications and candidate profiles from the files and directories below:

1. **Personal Candidate Profile:**
   - The candidate profile, contact details, education, and target preferences are defined in [CLAUDE.md](CLAUDE.md) and the individual profile methodology files under [.claude/skills/job-application-assistant/](.claude/skills/job-application-assistant/) (specifically `01-*.md` etc.).
2. **Canonical Workflow Specifications:**
   - The step-by-step instructions and triggers for tasks (setup, scrape, rank, apply, upskill, interview) are defined in the [.claude/](.claude/) directory (specifically under `.claude/skills/` and `.claude/commands/`).
   - Do not duplicate these rules or specifications. Treat `.claude/` files as the single source of truth.
3. **Unified Job Search Skill:**
   - [.agents/skills/search-jobs/](.agents/skills/search-jobs/) is the single portable job-search skill discovered by Codex and Antigravity. Its source adapters live under `sources/`; the canonical `/scrape` workflow in [.claude/skills/job-scraper/](.claude/skills/job-scraper/) orchestrates them together with direct company, ATS, aggregator, and web sources.

4. **Resume Design Source of Truth:**
   - [documents/cv/Adam Soliman Resume, 26-27.pdf](documents/cv/Adam%20Soliman%20Resume,%2026-27.pdf) is Adam's mandatory resume design master. Every new tailored resume must branch from this document and retain its exact one-page layout, font, font sizes, spacing, margins, section order, rules, and bullet treatment.
   - Tailoring may change only factual text content. Do not substitute `moderncv`, another stock template, a new visual system, or altered page geometry. If an editable source is unavailable and the original PDF cannot be reproduced exactly, request an editable source rather than silently changing the design.
