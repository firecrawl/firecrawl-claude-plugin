---
description: Search the web with Firecrawl and summarize the results with sources
argument-hint: <query>
disable-model-invocation: true
---

# Firecrawl search

Search for: $ARGUMENTS

Follow the `firecrawl` skill. Use `firecrawl_search` with the query and any
constraints the user gave (dates, sites, region). If no query was given, ask for
one. Read a result with `firecrawl_scrape` only when the answer needs more than
the excerpt. Cite the source URL for each claim.
