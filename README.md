# Firecrawl for Claude

Firecrawl is the context API for AI agents. This plugin connects Claude to
Firecrawl's hosted search tools to search the web, read the pages your searches
find, look up Alexandria data providers for structured data, and research
developer documentation, government publications, and scientific papers.

This plugin includes thirteen skills: three core search and research skills,
plus workflows for brand assets, business contacts, website design, professional
enrichment, lead discovery, fantasy sports, deep research, job openings,
developer documentation, and SEO audits. It connects to Firecrawl's hosted MCP
server, configured in `.mcp.json`.

## Install

In Claude.ai or Cowork, upload the plugin ZIP through **Customize > Plugins >
Add > Upload plugin**, then connect Firecrawl from the plugin's **Connectors**
tab. Installing a plugin and connecting its tools are separate steps.

In Claude Code, open `/plugin`, search for **firecrawl**, and install it.
The official marketplace controls which release is available there.

You can also add this repository directly as a marketplace:

```text
/plugin marketplace add firecrawl/firecrawl-claude-plugin
/plugin install firecrawl@firecrawl
```

Choose one installation of Firecrawl. If switching from the official marketplace
to this repository, disable the previous Firecrawl plugin first. After an
update, run `/reload-plugins` or start a new session, then use `/mcp` to complete
the account connection.

## Upgrading from 1.x

Version 2.0.0 connects to Firecrawl's hosted MCP server instead of the Firecrawl
CLI. You no longer need to install or authenticate the CLI for this plugin;
connect your account with `/mcp` instead.

The CLI skills (map, crawl, interact, monitor, agent, parse, download and the
other CLI commands) are no longer part of this plugin. To keep using them,
install them from the CLI's own skill distribution, either with:

```sh
npx skills add firecrawl/cli
```

or as a Claude Code plugin from the Firecrawl skills catalog:

```text
/plugin marketplace add firecrawl/skills
/plugin install firecrawl@firecrawl-skills
```

The CLI skills and this plugin both include skills named `firecrawl`,
`firecrawl-developer-index` and `firecrawl-research-index`. The CLI versions run
CLI commands and the versions here call MCP tools. If you install both, Claude
Code lists both.

## Commands

In Claude Code, the plugin also adds short commands:

- `/firecrawl:setup` checks the account connection and explains how to connect
  through `/mcp`.
- `/firecrawl:search <query>` searches the web and cites the results.
- `/firecrawl:scrape <url>` reads a page.
- `/firecrawl:map <site>` lists pages found on a site through search and its links.
- `/firecrawl:crawl <site>` reads several pages of a site and combines them.
- `/firecrawl:agent <question>` runs a cited multi-source investigation.

Plain requests work without a command; the skills choose the tools.

## Use

- Find recent sources on a topic and summarize them with citations.
- Read a supplied webpage and extract the requested information.
- Research a programming question using indexed repositories and documentation.
- Find scientific papers and read passages relevant to a question.
- Search US government publications and retrieve structured provider data.
- Gather a company's existing identity assets or document a website's design.
- Find business contacts, research one professional, or qualify a lead list.
- Verify job openings, compare fantasy options, or audit pages for SEO issues.
- Investigate a question across sources and produce a cited answer or report.

The skills report connection and authentication failures so you can reconnect
from the plugin's **Connectors** tab in Claude.ai and Cowork, or through `/mcp`
in Claude Code. Requests send search queries, page URLs, and requested provider
inputs to Firecrawl; include only the information needed for the task.

## Development

This repository is a generated distribution of the Firecrawl MCP plugin package.
Edits here are replaced by the next package release.

To validate a local checkout:

```sh
claude plugin validate .
claude --plugin-dir .
```

## Resources

- [Firecrawl documentation](https://docs.firecrawl.dev)
- [Firecrawl](https://www.firecrawl.dev)
- [Report a problem](https://github.com/firecrawl/firecrawl-claude-plugin/issues)

## License

MIT. See [LICENSE](LICENSE). The `firecrawl-deep-research` skill carries its own
ISC notice in [SKILL.md](skills/firecrawl-deep-research/SKILL.md).
