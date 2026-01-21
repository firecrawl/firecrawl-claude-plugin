---
description: Scrape a webpage and convert it to markdown using the Firecrawl CLI
allowed-tools: Bash
---

# Scrape Web Page

Use the Firecrawl CLI to extract content from a URL.

## Command Syntax

```bash
firecrawl scrape <url> [options]
firecrawl <url> [options]  # Shorthand
```

## Available Formats

Request different output formats with `-f, --format`:
- `markdown` - Clean markdown content (default)
- `html` - Raw HTML content
- `rawHtml` - Unprocessed HTML
- `screenshot` - Screenshot of the page
- `links` - Extract all links from the page
- `summary` - AI-generated summary of the content

Multiple formats can be combined: `--format "markdown,links"`

## When scraping:

1. If no URL is provided, ask the user for the URL they want to scrape
2. Ask what format they prefer if not specified (default to markdown)
3. Run the `firecrawl scrape` command with the URL and requested format
4. Return the content in a clean, readable format

## Options

| Option | Description |
|--------|-------------|
| `-f, --format <formats>` | Output format(s), comma-separated |
| `--only-main-content` | Extract only main content (excludes nav, footer) |
| `--wait-for <ms>` | Wait time for dynamic content in milliseconds |
| `--screenshot` | Take a screenshot of the page |
| `-o, --output <path>` | Write output to file |
| `--pretty` | Pretty print JSON output |

## Examples

```bash
firecrawl scrape https://example.com
firecrawl scrape https://example.com --format summary
firecrawl scrape https://example.com --format "markdown,links" --pretty
```
