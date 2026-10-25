---
description: Research a question across sources with Firecrawl and return a cited answer
argument-hint: <question or task>
disable-model-invocation: true
---

# Firecrawl agent

Research: $ARGUMENTS

Follow the `firecrawl-deep-research` skill, or a focused skill it names when one
fits the request better. If no question was given, ask for one. Start with the
smallest useful search, expand only for gaps that could change the answer, and
cite a source URL for each finding.
