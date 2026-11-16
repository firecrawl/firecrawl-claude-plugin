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

The same commands answer the other catalogue questions. For the providers of a
website, list the provider folders named after it, with its dots as hyphens,
such as `ls -d /library/*/*sec-gov*`, then the providers whose README names it:
`grep -rli "<domain>" /library --include=README.md | head -20`. For a data need
you can only describe, `cat /library/README.md` to pick the category and grep
several words for the need inside it, such as
`grep -rilE "rent|lease" /library/real-estate | head -20`.
These commands match names and text, so an empty result does not prove that no
provider covers the need: try another word, or the name of the site, before
concluding none does.

A contract states a credit price only where its provider wrote one into the
text; `alexandria_library_read` reports what a call charged as `creditsCost`.
Check the stated price and external effects against the user's request before
execution; a capability priced over the user's limit does not fit. If
access is unavailable or no capability fits, use
`firecrawl_search` and page retrieval where suitable. Read the executed result
before answering; a catalogue match alone does not supply the requested data.
