---
name: publish-llm-pages
description: Create, improve and publish Markdown pages for LLMs with the AIV connector, so they get a public .md URL and an entry in the site llms.txt. Use when the user wants an AI-friendly or Markdown version of a page, wants to write content for AI assistants, or asks to update or publish llms.txt entries.
---

# Publish Markdown pages for LLMs with AIV

Every published AIV document gets a public `.md` URL and an entry in the site llms.txt, which is
what AI assistants read. Drafts are private until published.

## Create a draft

Choose the source that fits the request:

- **From an existing page:** `create_document` with `source_url` (a page on the same domain).
  AIV converts the HTML to clean Markdown.
- **From text the user gives or you write together:** `create_document` with `markdown` and
  `title`.
- **Written by the AIV AI writer:** `generate_document` with a `topic`. This uses AI credits
  unless the account has the Own Key plan; check `get_account` and tell the user the cost first.

Use the site language unless the user asks for another (`lang`).

## Improve it

1. Read it back with `get_document`.
2. Run `analyze_content` with the `markdown` and, when known, the `keyphrase` the page should
   rank for.
3. Fix what the analysis flags: one H1, a clear first paragraph that answers the main question,
   short sections with descriptive headings, concrete facts (prices, numbers, dates), a short
   FAQ when it helps.
4. Save with `update_document`. Every save keeps the previous version as a revision.

## Publish

Show the user the final title and first lines and ask before publishing, because publishing
makes the page public. Then call `publish_document` and share `md_url` and the llms.txt URL.
`unpublish_document` takes a page down again; its content is kept.

If a tool reports that changes need the Own Key plan, tell the user and share the billing link
from the error instead of retrying.
