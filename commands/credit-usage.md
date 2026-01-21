---
description: Check remaining Firecrawl API credits
allowed-tools: Bash
---

# Check Credit Usage

Use the Firecrawl CLI to check your remaining API credits.

## Command Syntax

```bash
firecrawl credit-usage [options]
```

## Options

| Option | Description |
|--------|-------------|
| `--json` | Output as JSON format |
| `--pretty` | Pretty print JSON output |
| `-o, --output <path>` | Write output to file |

## Examples

```bash
firecrawl credit-usage
firecrawl credit-usage --json --pretty
firecrawl credit-usage -o credits.json
```
