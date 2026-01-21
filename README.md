# Firecrawl Plugin for Claude Code

Turn any website into clean, LLM-ready markdown or structured data with the Firecrawl CLI.

## Features

- **Scrape**: Extract content from any webpage as clean markdown
- **Crawl**: Automatically discover and extract content from entire websites
- **Map**: Discover all URLs on a website
- **Credit Usage**: Check your remaining API credits

All features include automatic JavaScript rendering, anti-bot handling, and proxy rotation.

## Installation

### 1. Install the Plugin

```
/plugin install firecrawl@claude-plugins-official
```

**Important:** After installing, restart Claude Code to load the plugin.

### 2. Set Up the CLI and API Key

Run `/firecrawl:setup` to install the Firecrawl CLI and configure your API key.

**Get your free API key at:** https://firecrawl.dev/app/api-keys

### 3. Verify Setup

Run `/firecrawl:setup` again to confirm everything is working.

## Usage

### Slash Commands

| Command | Description |
|---------|-------------|
| `/firecrawl:setup` | Install CLI and configure API key |
| `/firecrawl:scrape` | Scrape a single webpage to markdown |
| `/firecrawl:crawl` | Crawl an entire website |
| `/firecrawl:map` | Discover all URLs on a website |
| `/firecrawl:credit-usage` | Check remaining API credits |
| `/firecrawl:version` | Check CLI version |

### Available Formats

When scraping, you can request different output formats:
- `markdown` - Clean markdown content (default)
- `html` - Raw HTML content
- `screenshot` - Screenshot of the page
- `links` - Extract all links
- `summary` - AI-generated summary

### Examples

**Scrape a documentation page:**
```
Scrape https://docs.firecrawl.dev/introduction and summarize the key points
```

**Get a summary of a page:**
```
/firecrawl:scrape https://firecrawl.dev --format summary
```

**Crawl a documentation site:**
```
/firecrawl:crawl https://docs.firecrawl.dev --wait --limit 20
```

**Discover site structure:**
```
/firecrawl:map https://firecrawl.dev
```

## Configuration

### Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `FIRECRAWL_API_KEY` | Yes | Your Firecrawl API key |
| `FIRECRAWL_API_URL` | No | Custom API endpoint (for self-hosted) |

## Self-Hosted Deployment

Firecrawl can be self-hosted. Set `FIRECRAWL_API_URL` to point to your instance:

```bash
export FIRECRAWL_API_URL=https://your-firecrawl-instance.com
```

See [Firecrawl documentation](https://docs.firecrawl.dev) for self-hosting instructions.

## Local Development

To test or develop this plugin locally:

### 1. Add the local marketplace

```bash
claude plugin marketplace add /path/to/firecrawl-claude-plugin/.claude-plugin/marketplace.json
```

### 2. Install the plugin

```bash
claude plugin install firecrawl@firecrawl-local
```

### (removing)

```bash
claude plugin uninstall firecrawl@firecrawl-local
```
### 3. Restart Claude Code

After installation, restart Claude Code and your `/firecrawl:` commands will be available.

## Resources

- [Firecrawl Documentation](https://docs.firecrawl.dev)
- [Firecrawl CLI](https://github.com/mendableai/firecrawl-cli)
- [API Reference](https://docs.firecrawl.dev/api-reference)
- [GitHub Repository](https://github.com/mendableai/firecrawl)
- [Get API Key](https://firecrawl.dev)

## License

This plugin is licensed under AGPL-3.0, consistent with Firecrawl's open-source license.

## Support

- [Firecrawl Discord](https://discord.gg/gSmWdAkdwd)
- [GitHub Issues](https://github.com/mendableai/firecrawl/issues)
- Email: hello@firecrawl.dev
