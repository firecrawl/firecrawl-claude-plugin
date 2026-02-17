# Firecrawl Plugin for Claude Code

Turn any website into clean, LLM-ready markdown or structured data — directly from Claude Code.

This plugin adds the [Firecrawl CLI](https://github.com/firecrawl/cli) as a skill to Claude Code, giving it the ability to scrape, search, crawl, and map the web.

## Features

- **Search** - Web search with optional scraping of results (supports web, news, and image sources)
- **Scrape** - Extract clean markdown content from any webpage, with JavaScript rendering
- **Map** - Discover all URLs on a website
- **Crawl** - Extract content from entire websites
- **Browser** - Launch cloud browser sessions and execute Playwright code remotely

All operations include automatic JavaScript rendering, anti-bot handling, and proxy rotation.

## Installation

### 1. Install the Plugin

In Claude Code, run `/plugin` and search for **firecrawl**, then select it to install.

### 2. Install the Firecrawl CLI

The plugin requires the Firecrawl CLI to be installed globally:

```bash
npm install -g firecrawl-cli
```

### 3. Authenticate

Run the following to authenticate via your browser:

```bash
firecrawl login --browser
```

Or authenticate with an API key directly:

```bash
firecrawl login --api-key "fc-YOUR-API-KEY"
```

You can also set the key as an environment variable (add to `~/.zshrc` or `~/.bashrc` for persistence):

```bash
export FIRECRAWL_API_KEY=fc-YOUR-API-KEY
```

**Get your free API key at:** https://firecrawl.dev/app/api-keys

### 4. Verify Setup

```bash
firecrawl --status
```

You should see your authentication status, concurrency limit, and remaining credits.

## Usage

Once installed, Claude Code will automatically use Firecrawl for web tasks. Just ask naturally:

**Search the web:**
```
Search for "best practices for React testing" and compile the key recommendations
```

**Scrape a page:**
```
Scrape https://docs.firecrawl.dev/introduction and summarize the key points
```

**Discover site structure:**
```
Map all URLs on https://firecrawl.dev
```

**Research a topic:**
```
Research the latest developments in AI agents and give me a summary
```

### CLI Commands

The plugin uses these Firecrawl CLI commands under the hood:

| Command | Description |
|---------|-------------|
| `firecrawl search "query"` | Search the web (supports `--sources`, `--scrape`, `--tbs` for time filters) |
| `firecrawl scrape <url>` | Scrape a single page to markdown |
| `firecrawl map <url>` | Discover all URLs on a site |
| `firecrawl browser launch/execute/list/close` | Manage cloud browser sessions and execute Playwright code |
| `firecrawl --status` | Check auth status, concurrency, and credits |

### Output Files

Results are saved to a `.firecrawl/` directory in your project to keep Claude Code's context window clean:

```
.firecrawl/search-react_server_components.json
.firecrawl/docs.github.com-actions-overview.md
.firecrawl/firecrawl.dev.md
```

## Configuration

| Variable | Required | Description |
|----------|----------|-------------|
| `FIRECRAWL_API_KEY` | Yes (if not using `firecrawl login`) | Your Firecrawl API key |
| `FIRECRAWL_API_URL` | No | Custom API endpoint (for self-hosted instances) |

## Self-Hosted Deployment

Firecrawl can be self-hosted. Set `FIRECRAWL_API_URL` to point to your instance:

```bash
export FIRECRAWL_API_URL=https://your-firecrawl-instance.com
```

See the [Firecrawl documentation](https://docs.firecrawl.dev) for self-hosting instructions.

## Resources

- [Firecrawl Documentation](https://docs.firecrawl.dev)
- [Firecrawl CLI Repository](https://github.com/firecrawl/cli)
- [API Reference](https://docs.firecrawl.dev/api-reference)
- [Get API Key](https://firecrawl.dev)

## License

This plugin is licensed under AGPL-3.0, consistent with Firecrawl's open-source license.

## Support

- [Firecrawl Discord](https://discord.gg/gSmWdAkdwd)
- [GitHub Issues](https://github.com/mendableai/firecrawl/issues)
- Email: hello@firecrawl.dev
