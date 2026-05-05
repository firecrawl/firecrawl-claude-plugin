---
name: firecrawl-parse
description: |
  Parse local or non-public documents with Firecrawl /v2/parse. Use this skill when the user provides a local file path or asks to parse, read, convert, summarize, or ask questions about a document on disk, including PDF, DOCX, DOC, ODT, RTF, XLSX, XLS, HTML, or HTM files. Prefer this over scrape for local files; use scrape instead when the source is a public document URL.
allowed-tools:
  - Bash(firecrawl *)
  - Bash(npx firecrawl *)
---

# firecrawl parse

Turn a local document into clean, LLM-ready output with Firecrawl `/v2/parse`. Supports `.pdf`, `.docx`, `.doc`, `.odt`, `.rtf`, `.xlsx`, `.xls`, `.html`, and `.htm` files.

## When to use

- The source is a file on disk, uploaded by the user, or otherwise not publicly accessible by URL
- The user asks to parse, read, convert, summarize, or ask questions about a local document
- Use `firecrawl scrape` instead when the source is a public URL to a document; scrape auto-detects supported document files from extension or content type

## Quick start

Always write parse output to `.firecrawl/` with `-o`; parsed documents can be large.

```bash
mkdir -p .firecrawl

# File to markdown
firecrawl parse "./report.pdf" -o .firecrawl/report.md

# Include multiple output formats
firecrawl parse "./report.pdf" --format markdown,links --json --pretty \
  -o .firecrawl/report.json

# Summary
firecrawl parse "./contract.docx" --summary -o .firecrawl/contract-summary.md

# Ask a question about the document
firecrawl parse "./invoice.pdf" --query "What is the total amount due?" \
  -o .firecrawl/invoice-answer.md
```

Read outputs incrementally with `head`, `rg`, `wc`, or `sed` instead of loading large files all at once.

## Options

| Option | Description |
| --- | --- |
| `-f, --format <formats>` | Output formats: `markdown`, `html`, `rawHtml`, `links`, `images`, `summary`, `json`, `attributes` |
| `-H, --html` | Shortcut for `--format html` |
| `-S, --summary` | Shortcut for `--format summary` |
| `-Q, --query <prompt>` | Ask a question about the parsed content |
| `--only-main-content` | Include only main content |
| `--include-tags <tags>` | Comma-separated HTML tags to include |
| `--exclude-tags <tags>` | Comma-separated HTML tags to exclude |
| `--timeout <ms>` | Timeout for the parse job |
| `--json` | Emit JSON output |
| `--pretty` | Pretty-print JSON output |
| `-o, --output <path>` | Output file path; prefer `.firecrawl/` |

## Tips

- Quote paths with spaces: `firecrawl parse "./My Report.pdf" -o .firecrawl/my-report.md`.
- Max upload size is 50 MB per request.
- `/v2/parse` accepts local file bytes via multipart form upload. Do not print API keys or multipart payloads to logs.
- For public PDF, DOCX, XLSX, or HTML URLs, prefer `firecrawl scrape "<url>" -o .firecrawl/page.md`.
- Check `.firecrawl/` before parsing the same file again.
- Check credits before batch work with `firecrawl credit-usage`.

## See also

- [firecrawl-scrape](../firecrawl-scrape/SKILL.md) - parse document URLs or scrape webpages
- [firecrawl-cli](../firecrawl-cli/SKILL.md) - full Firecrawl CLI workflow
