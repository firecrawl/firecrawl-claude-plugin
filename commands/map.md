---
description: Discover all URLs on a website using the Firecrawl CLI
allowed-tools: Bash
---

# Map Website URLs

Use the Firecrawl CLI to discover all accessible URLs on a website.

## Command Syntax

```bash
firecrawl map <url> [options]
```

## When mapping:

1. Take the starting URL from the user
2. Run `firecrawl map` to discover all pages
3. Present the URL structure in an organized way
4. Offer to crawl or scrape specific discovered pages

## Options

| Option | Description |
|--------|-------------|
| `--limit <number>` | Maximum URLs to discover (default: 100) |
| `--search <query>` | Filter URLs containing specific text |
| `--sitemap <mode>` | Sitemap handling: `include`, `skip`, or `only` |
| `--include-subdomains` | Include URLs from subdomains |
| `-o, --output <path>` | Write output to file |
| `--json` | Output as JSON (default: one URL per line) |

## Examples

```bash
firecrawl map https://firecrawl.dev
firecrawl map https://docs.example.com --limit 50 --search "api"
firecrawl map https://example.com --json -o sitemap.json
```
