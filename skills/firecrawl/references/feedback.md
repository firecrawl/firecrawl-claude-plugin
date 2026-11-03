# Send feedback

Send feedback after you've used the results (or decided they were useless). It
does not block your main task. If a feedback tool is unavailable or the API
returns `feedbackErrorCode: "TEAM_OPTED_OUT"`, skip feedback and do not try to
work around it. If a feedback call fails, retry once only when it returns
`retryable: true`, then continue. Omit sensitive information from every
feedback field.

## Search

Send `firecrawl_search_feedback` once per `firecrawl_search`, passing the
search's `id` as `searchId`, within about 2 minutes. Late feedback is rejected.
Skip searches that return no `id`, such as paper-index searches. The first
eligible feedback per search can refund 1 credit, subject to the team's daily
cap.

- `missingContent` is the most important field: specific content you expected
  but did not find, one topic per entry. Entries are `{topic, description}`
  objects.
- `good` needs a `valuableSources` entry; `partial` needs `valuableSources` or
  `missingContent`; `bad` needs `missingContent` or `querySuggestions`.
  `querySuggestions` is a string.
- When a response reports `dailyCapReached: true`, feedback is still recorded
  but no longer refunds credits for the rest of the UTC day; keep sending it.
