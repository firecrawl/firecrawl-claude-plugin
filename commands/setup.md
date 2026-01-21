---
description: Set up Firecrawl CLI and configure API key
allowed-tools: Bash, AskUserQuestion
---

# Firecrawl Setup

Install and configure the Firecrawl CLI.

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
npm install -g firecrawl-cli@beta
```

If permission denied:
```bash
sudo npm install -g firecrawl-cli@beta
```

If npm is NOT available, tell the user to install Node.js from https://nodejs.org

## Step 3: Check if already configured

```bash
firecrawl credit-usage 2>&1
```

If this returns credit information, the CLI is already configured - skip to Step 5.

If it shows the auth prompt, proceed to Step 4.

## Step 4: Configure API key

Use `AskUserQuestion` to ask the user how they want to authenticate:

**Question:** "How would you like to authenticate with Firecrawl?"
**Options:**
1. "Login with browser (recommended)" - Opens browser to authenticate
2. "Enter API key manually" - Paste an existing API key

**If browser login:**
Tell the user to run `firecrawl config` in their terminal and select option 1. The browser will open for authentication.

**If manual API key:**
Use `AskUserQuestion` to ask for their API key, then set it:
```bash
export FIRECRAWL_API_KEY="<their-key>" && firecrawl credit-usage
```

If it works, tell them to add this to their shell profile (~/.zshrc or ~/.bashrc) for persistence.

**Get an API key at:** https://firecrawl.dev/app/api-keys

## Step 5: Verify setup

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
| `command not found: firecrawl` | Run `npm install -g firecrawl-cli@beta` |
| `command not found: npm` | Install Node.js from https://nodejs.org |
| `EACCES: permission denied` | Run `sudo npm install -g firecrawl-cli@beta` |
| `401 Unauthorized` | Run `firecrawl config` to re-authenticate |
