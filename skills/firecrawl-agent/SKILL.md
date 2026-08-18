---
name: firecrawl-agent
description: |
  AI-powered autonomous data extraction that navigates complex sites and returns structured JSON. Use this skill when the user wants structured data from websites, needs to extract pricing tiers, product listings, directory entries, or any data as JSON with a schema. Triggers on "extract structured data", "get all the products", "pull pricing info", "extract as JSON", or when the user provides a JSON schema for website data. More powerful than simple scraping for multi-page structured extraction.
allowed-tools:
  - Bash(firecrawl *)
  - Bash(npx firecrawl-cli *)
---

# firecrawl agent

AI-powered autonomous extraction. The agent navigates sites and extracts structured data (takes 2-5 minutes).

## When to use

- You need structured data from complex multi-page sites
- Manual scraping would require navigating many pages
- You want the AI to figure out where the data lives

## Quick start

```bash
# Extract structured data
firecrawl agent "extract all pricing tiers" --wait --json -o .firecrawl/pricing.json

# With a JSON schema for structured output
firecrawl agent "extract products" --schema '{"type":"object","properties":{"name":{"type":"string"},"price":{"type":"number"}}}' --wait --json -o .firecrawl/products.json

# Focus on specific pages
firecrawl agent "get feature list" --urls "<url>" --wait --json -o .firecrawl/features.json
```

## Job IDs

Without `--wait`, the command returns a job ID. A UUID positional argument is auto-detected as a status check:

```bash
# Check once (equivalent to adding --status)
firecrawl agent "<job-id>"

# Wait on an existing job, polling every 10 seconds for up to 5 minutes
firecrawl agent "<job-id>" --wait --poll-interval 10 --timeout 300

# Cancel an active job
firecrawl agent "<job-id>" --cancel
```

## Options

| Option                      | Description                                           |
| --------------------------- | ----------------------------------------------------- |
| `--urls <urls>`             | Starting URLs for the agent                           |
| `--model <model>`           | Model to use: spark-1-mini or spark-1-pro             |
| `--schema <json>`           | JSON schema for structured output                     |
| `--schema-file <path>`      | Path to JSON schema file                              |
| `--max-credits <n>`         | Credit limit for this agent run                       |
| `--status`                  | Check a job ID's status                               |
| `--cancel`                  | Cancel an active job ID                               |
| `--wait`                    | Wait for agent to complete                            |
| `--poll-interval <seconds>` | Polling interval while waiting (default: 5 seconds)   |
| `--timeout <seconds>`       | Stop waiting after this duration (default: none)      |
| `--json`                    | Output as JSON                                        |
| `--pretty`                  | Pretty print JSON (`--wait` results require `--json`) |
| `-o, --output <path>`       | Output file path                                      |

## Tips

- Use `--wait` for inline results; without it you get a job ID (see [Job IDs](#job-ids)).
- Use `--schema` for predictable, structured output — otherwise the agent returns freeform data.
- Agent runs consume more credits than simple scrapes. Use `--max-credits` to cap spending.
- For simple single-page extraction, prefer `scrape` — it's faster and cheaper.

## See also

- [firecrawl-scrape](../firecrawl-scrape/SKILL.md) — simpler single-page extraction
- [firecrawl-interact](../firecrawl-interact/SKILL.md) — scrape + interact for manual page interaction (more control)
- [firecrawl-crawl](../firecrawl-crawl/SKILL.md) — bulk extraction without AI
