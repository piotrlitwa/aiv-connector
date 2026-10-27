# AIV - AI Visibility

The `aiv` MCP server connects to the user's AIV account (https://aiv.piotrlitwa.com). AIV audits
website URLs for AI readiness (0-100 score: Markdown version, canonical, JSON-LD, H1, meta),
serves llms.txt and hosts Markdown pages for LLMs.

- Start with `list_sites`; most tools take a `site` (domain) argument.
- Audit: `get_site_overview`, then `list_urls` with `filter` `low_score`, `missing_md` or
  `errors`, then `get_url_audit` for details. Report a prioritised fix list with exact numbers.
- Content: `create_document` (from `markdown` or a `source_url` on the site) or
  `generate_document` (uses AI credits), check with `analyze_content`, save with
  `update_document`, and publish with `publish_document` only after the user confirms, since
  publishing makes the page public and adds it to llms.txt.
- Changes require the Own Key plan; on a read-only plan, share the billing link from the error.
- Authentication is OAuth: if tools fail with an authentication error, run `/mcp auth aiv`.
