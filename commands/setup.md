---
description: Set up Firecrawl CLI and configure API key
allowed-tools: Bash
---

# Firecrawl Setup

Automatically install and configure the Firecrawl CLI.

## Step 1: Check if CLI is installed

```bash
firecrawl version 2>/dev/null || echo "NOT_INSTALLED"
```

## Step 2: Install if needed

If not installed, first check if npm is available:
```bash
npm --version 2>/dev/null || echo "NPM_NOT_FOUND"
```

If npm is available, install:
```bash
npm install -g firecrawl-cli
```

If permission denied:
```bash
sudo npm install -g firecrawl-cli
```

If npm is NOT available, tell the user to install Node.js from https://nodejs.org

## Step 3: Configure API key

Ask the user for their API key (get one at https://firecrawl.dev/app/api-keys)

Test it directly:
```bash
FIRECRAWL_API_KEY="<user-provided-key>" firecrawl scrape https://firecrawl.dev --format summary
```

If it works, save it permanently to their shell config:
```bash
echo 'export FIRECRAWL_API_KEY="fc-their-key"' >> ~/.zshrc
```

## Step 4: Verify setup

```bash
firecrawl credit-usage
```

## Success Message

"Firecrawl CLI is installed and configured! You can now use:
- `/firecrawl:scrape` - Scrape a single page
- `/firecrawl:crawl` - Crawl an entire website
- `/firecrawl:map` - Discover URLs on a site"

## Troubleshooting

| Issue | Solution |
|-------|----------|
| `command not found: firecrawl` | Run `npm install -g firecrawl-cli` |
| `command not found: npm` | Install Node.js from https://nodejs.org |
| `EACCES: permission denied` | Run `sudo npm install -g firecrawl-cli` |
| `401 Unauthorized` | Invalid API key - get one at https://firecrawl.dev/app/api-keys |
