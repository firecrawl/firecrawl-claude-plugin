# Retrieve data-provider records

Search results can include provider suggestions in `data.tools`. These describe
capabilities; they are not executed results. `alexandria_library_search` explores the
provider library as read-only files with shell commands and reads contracts. It
does not discover this host's MCP tools.

Inspect the selected provider and capability with `alexandria_library_search` when
the full contract is not already available: `grep -ril "<term>" /library | head -20`
finds capabilities, `cat /library/<category>/README.md` lists a category's providers,
and `cat /library/<category>/<provider>/<capability>.md` reads one contract, whose
path names the provider and capability. Use its input contract to
build `options`, and execute with `alexandria_library_read` using
`calls: [{provider, capability, options}]`. Preserve returned identifiers;
do not invent provider names, capability names, or required inputs.

`firecrawl_find_tools` answers the catalogue questions the library files do
not: `urls` finds the providers for a website, `query` matches a data need by
meaning, and `includeCosts: true` returns each capability's listed credit price.

Check the capability's stated price and external effects against the user's
request before execution; a capability priced over the user's limit does not
fit. If access is unavailable or no capability fits, use
`firecrawl_search` and page retrieval where suitable. Read the executed result
before answering; a catalogue match alone does not supply the requested data.
