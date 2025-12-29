---
description: Use AI agent for autonomous web data gathering
allowed-tools: firecrawl_agent, firecrawl_agent_status
---

# AI Agent for Web Data Gathering

Use the Firecrawl AI agent to autonomously search, navigate, and extract data from the web.

## When to use the agent:

1. Take the user's data request in natural language
2. Use `firecrawl_agent` with a clear prompt describing what data is needed
3. Poll `firecrawl_agent_status` until the job completes
4. Present the extracted data in a clear format

## Key advantages over other tools:

- **No URLs required** - just describe what you need
- **Autonomous navigation** - agent finds and follows relevant links
- **Multi-source gathering** - collects data from multiple pages/sites
- **Structured output** - returns data matching your schema

## Options

- `prompt`: Natural language description of the data you want (required)
- `urls`: Optional array of URLs to focus the agent on specific pages
- `schema`: Optional JSON schema for structured output

## Example prompts:

- "Find the top 5 AI startups founded in 2024 and their funding amounts"
- "Get the pricing information for Firecrawl, Apify, and ScrapingBee"
- "Find the founders of Anthropic and their backgrounds"

## Use cases

- Complex research requiring multiple sources
- Competitive analysis across multiple websites
- Gathering structured data without knowing exact URLs
- Data extraction tasks that would require multiple scrape/search calls
