---
description: Connect your Firecrawl account and check that the Firecrawl tools respond
disable-model-invocation: true
---

# Firecrawl setup

This plugin connects to Firecrawl's hosted MCP server. It needs no API key in
the conversation and no CLI install.

1. Check whether the Firecrawl tools are available in this session. If they are,
   make one free call, `firecrawl_find_tools` with a short query, to confirm the
   account connection works.
2. If the tools are missing or the call reports a connection or authentication
   error, tell the user to run `/mcp`, select **firecrawl**, and complete the
   sign-in in the browser, then run `/firecrawl:setup` again.
3. Never ask the user to paste an API key into the conversation.

When the check passes, say which commands are available: `/firecrawl:search`,
`/firecrawl:scrape`, `/firecrawl:map`, `/firecrawl:crawl` and
`/firecrawl:agent`. Plain requests work too; the `firecrawl` skill picks the
right tool.
