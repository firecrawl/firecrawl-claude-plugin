---
description: Crawl an entire website and extract content from multiple pages using the Firecrawl CLI
allowed-tools: Bash
---

# Crawl Website

Use the Firecrawl CLI to extract content from multiple pages of a website.

## Command Syntax

```bash
firecrawl crawl <url> [options]
firecrawl crawl <job-id>  # Check status of existing crawl
```

## Important: Use --wait for automatic completion

Crawl operations are asynchronous. **Always use `--wait`** to automatically wait for completion:

```bash
firecrawl crawl https://example.com --wait --progress
```

Do NOT ask the user to check status manually - handle it automatically with `--wait`.

## When crawling:

1. Ask the user for the starting URL if not provided
2. Clarify the scope: how many pages, specific sections, or entire site
3. Run `firecrawl crawl` with `--wait --progress` and appropriate limits
4. Summarize the crawled content and provide structured results

## Options

| Option | Description |
|--------|-------------|
| `--wait` | Wait for crawl to complete before returning |
| `--progress` | Show progress while waiting |
| `--limit <number>` | Maximum number of pages to crawl |
| `--max-depth <number>` | Maximum crawl depth |
| `--include-paths <paths>` | Comma-separated URL patterns to include |
| `--exclude-paths <paths>` | Comma-separated URL patterns to exclude |
| `-o, --output <path>` | Write output to file |

## Examples

```bash
firecrawl crawl https://docs.example.com --wait --progress
firecrawl crawl https://example.com --wait --limit 50 --max-depth 3
firecrawl crawl https://example.com --wait --include-paths "blog,docs"
```
