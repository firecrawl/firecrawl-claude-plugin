---
name: web-scraping
description: Enables intelligent web scraping and data extraction using the Firecrawl CLI. Use when extracting content from web pages, crawling sites, or discovering URLs.
---

# Web Scraping with Firecrawl CLI

This skill enables intelligent web scraping and data extraction using the Firecrawl command-line interface.

## When to Use

Use the Firecrawl CLI when you need to:
- Extract content from web pages and convert to markdown
- Crawl multiple pages from a website
- Discover all URLs on a website (sitemap generation)
- Get summaries, screenshots, or links from web pages

## Available CLI Commands

### firecrawl scrape
Scrape a single URL and return clean content.

```bash
firecrawl scrape <url> [options]
firecrawl <url> [options]  # Shorthand
```

**Key options:**
- `-f, --format <formats>` - Output format(s): markdown, html, rawHtml, links, screenshot, summary, json, branding
- `--only-main-content` - Extract only main content (excludes nav, footer)
- `--wait-for <ms>` - Wait time for dynamic content
- `--screenshot` - Take a screenshot
- `-o, --output <path>` - Write to file
- `--pretty` - Pretty print JSON output

### firecrawl crawl
Crawl an entire website starting from a URL.

```bash
firecrawl crawl <url> [options]
firecrawl crawl <job-id>  # Check status
```

**Key options:**
- `--wait` - Wait for crawl to complete
- `--progress` - Show progress while waiting
- `--limit <n>` - Maximum pages to crawl
- `--max-depth <n>` - Maximum crawl depth
- `--include-paths <paths>` - URL patterns to include
- `--exclude-paths <paths>` - URL patterns to exclude
- `--timeout <seconds>` - Maximum wait time
- `-o, --output <path>` - Write to file

### firecrawl map
Discover all URLs on a website.

```bash
firecrawl map <url> [options]
```

**Key options:**
- `--limit <n>` - Maximum URLs to discover (default: 100)
- `--search <query>` - Filter URLs by text
- `--sitemap <mode>` - Sitemap handling: include, skip, only
- `--include-subdomains` - Include subdomains
- `--json` - Output as JSON
- `-o, --output <path>` - Write to file

### firecrawl config
Configure API key and settings interactively.

```bash
firecrawl config
```

### firecrawl credit-usage
Check remaining API credits.

```bash
firecrawl credit-usage [options]
```

**Options:**
- `--json` - Output as JSON
- `--pretty` - Pretty print JSON

### firecrawl version
Display CLI version.

```bash
firecrawl version
```

## Available Output Formats

When scraping, you can request different output formats:
- `markdown` - Clean markdown content (default)
- `html` - Raw HTML content
- `rawHtml` - Unprocessed HTML
- `screenshot` - Screenshot of the page
- `links` - Extract all links from the page
- `summary` - AI-generated summary of the content
- `json` - Structured JSON output
- `branding` - Brand identity (colors, fonts, typography)

## Best Practices

1. **Start with map**: For large sites, use `firecrawl map` first to understand the site structure

2. **Use appropriate command**:
   - Known single URL → `firecrawl scrape <url>`
   - Multiple pages from a site → `firecrawl crawl <url>`
   - Discover site structure → `firecrawl map <url>`

3. **Use --wait for crawls**: Always use `--wait --progress` to automatically wait for completion rather than polling manually

4. **Choose the right format**: Use `--format summary` for quick overviews, `--format markdown` for full content, `--format links` for navigation analysis

5. **Handle rate limits**: Use `firecrawl credit-usage` to check remaining credits before large operations

6. **JavaScript-rendered content**: Use `--wait-for <ms>` if the page needs time to render dynamic content

## Example Workflows

### Research Task
```bash
# Scrape a single page for content
firecrawl scrape https://example.com/article --format markdown

# Get a quick summary
firecrawl scrape https://example.com --format summary
```

### Documentation Extraction
```bash
# First, discover all documentation pages
firecrawl map https://docs.example.com --limit 50

# Then crawl the docs with limits
firecrawl crawl https://docs.example.com --wait --progress --limit 20 --max-depth 3
```

### Quick Page Summary
```bash
# Get AI-generated summary
firecrawl scrape https://example.com --format summary

# If more detail needed, get full markdown
firecrawl scrape https://example.com --format markdown
```

### Site Analysis
```bash
# Map the entire site structure
firecrawl map https://example.com --json --pretty -o sitemap.json

# Get screenshots of key pages
firecrawl scrape https://example.com --screenshot -o homepage.json
```

## Global Options

These work with all commands:
- `-k, --api-key <key>` - Override configured API key
- `-o, --output <path>` - Write output to file
- `--pretty` - Pretty print JSON output
- `-h, --help` - Display help for command
