---
description: Extract structured data from web pages
allowed-tools: firecrawl_extract
---

# Structured Data Extraction

Use Firecrawl extract to pull specific structured data from web pages using LLM.

## When to use extract:

1. Identify the URLs containing the data
2. Define what fields you want to extract
3. Use `firecrawl_extract` with a schema
4. Return the structured data to the user

## Options

- `urls`: Array of URLs to extract from (required)
- `prompt`: Description of what to extract
- `schema`: JSON schema defining the structure of data to extract
- `allowExternalLinks`: Allow extraction from linked pages
- `enableWebSearch`: Enable web search for additional context
- `includeSubdomains`: Include subdomains in extraction

## Example schema:

```json
{
  "type": "object",
  "properties": {
    "name": { "type": "string" },
    "price": { "type": "number" },
    "description": { "type": "string" }
  },
  "required": ["name", "price"]
}
```

## Use cases

- Extracting product information (name, price, specs)
- Pulling contact details from company pages
- Gathering structured data from multiple similar pages
- Converting unstructured web content into JSON
