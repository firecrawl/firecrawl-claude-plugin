# Firecrawl for Claude Code

Search the web, read source pages, retrieve structured data, and research
developer documentation, government publications, and scientific papers using
Firecrawl's hosted MCP tools.

This plugin includes three skills: `firecrawl`, `firecrawl-developer-index`,
and `firecrawl-research-index`. It connects to Firecrawl's hosted MCP server
(configured in `.mcp.json`). Connect your Firecrawl account through Claude
Code's `/mcp` menu before using the tools.

## Install

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

## Use

- Find recent sources on a topic and summarize them with citations.
- Read a supplied webpage and extract the requested information.
- Research a programming question using indexed repositories and documentation.
- Find scientific papers and read passages relevant to a question.
- Search US government publications and retrieve structured provider data.

The skills report connection and authentication failures so you can reconnect
through `/mcp`.

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

MIT. See [LICENSE](LICENSE).
