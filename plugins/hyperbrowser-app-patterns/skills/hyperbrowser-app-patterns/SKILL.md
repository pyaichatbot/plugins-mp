---
name: hyperbrowser-app-patterns
description: Use when building, reviewing, or extending Hyperbrowser-based web automation, scraping, crawling, screenshot analysis, competitor tracking, research, site-to-dataset, or web-to-agent applications.
license: NOASSERTION
---

# Hyperbrowser App Patterns

Use this skill to build production-style applications with `@hyperbrowser/sdk` using patterns curated from `hyperbrowserai/hyperbrowser-app-examples`.

This is a pattern plugin, not a bulk copy of every app in the source repository. Use the references to choose an app archetype and implement the smallest reliable workflow for the user request.

## When To Use

Use this skill when a task involves:

- Browser automation with Hyperbrowser sessions.
- Web scraping, crawl, or extraction workflows.
- Screenshot or UI analysis apps.
- Competitor tracking and page diffing.
- Deep research apps over websites, Reddit, jobs, companies, or docs.
- Turning a website into typed agent tools.
- Creating datasets from site content.

## Core Integration Rules

- Load `HYPERBROWSER_API_KEY` from environment or server-side config only.
- Keep Hyperbrowser SDK calls server-side; do not expose API keys to browser clients.
- Validate request bodies with a schema before starting crawl/scrape/session work.
- Add retry/backoff around network and browser operations.
- Bound crawl depth, page count, content size, and runtime.
- Clean up sessions in `finally` blocks when using session APIs.
- Return structured JSON with `success`, `data`, and `error` fields from API routes.
- Log enough progress for long-running crawls without leaking secrets.

## Common App Archetypes

### Crawl and Extract

Use for documentation crawlers, site-to-dataset, content ingestion, and research apps.

Pattern:

1. Validate URL and crawl options.
2. Start with one URL and a bounded queue.
3. Scrape HTML or markdown with Hyperbrowser.
4. Extract links and filter by domain/include/exclude patterns.
5. Chunk or normalize content.
6. Return per-page results and errors.

Reference snippets:

- `references/selected-snippets/site-to-dataset-crawler.ts`
- `references/selected-snippets/competitor-crawl.ts`

### Website to Agent Tools

Use when generating typed functions that interact with a target website.

Pattern:

1. Crawl target page and extract interactive elements.
2. Ask an LLM to generate TypeScript tool functions using only official Hyperbrowser session methods.
3. Require Zod schemas for every generated tool input.
4. Create a stealth session, navigate, act, capture screenshot or HTML, and close the session.
5. Review generated code before execution.

Reference snippets:

- `references/selected-snippets/web-to-agent-hyperbrowser.ts`
- `references/selected-snippets/web-to-agent-scaffold-route.ts`

### Competitor Tracking

Use for recurring page monitoring and diff summaries.

Pattern:

1. Scrape target URLs with stealth and adblock options.
2. Store previous HTML snapshots.
3. Diff current and previous content.
4. Summarize meaningful changes with an LLM.
5. Notify through configured channels.

### Research Apps

Use for Reddit research, job research, YC/company research, source discovery, and topic research.

Pattern:

1. Normalize a user query or target URL.
2. Gather content from bounded sources.
3. Deduplicate and score findings.
4. Produce structured artifacts: tables, reports, datasets, pages, or exports.
5. Make provenance visible in final output.

## Review Checklist

Before shipping a Hyperbrowser app:

- API keys are server-only and never returned to clients.
- Crawl/scrape jobs have max pages, depth, timeout, and content limits.
- Session lifecycle is explicit and cleanup is reliable.
- User-provided URLs are validated and SSRF-sensitive environments are considered.
- Long-running jobs expose progress or polling/streaming status.
- Failures return structured errors with retryable/non-retryable distinction when useful.
- Generated tools or code are reviewed before execution.

## References

- Examples index: `references/examples-index.md`
- SDK and workflow patterns: `references/sdk-patterns.md`
- Selected snippets: `references/selected-snippets/`
- Upstream README: `../../references-upstream-README.md`
- Upstream repository: https://github.com/hyperbrowserai/hyperbrowser-app-examples
