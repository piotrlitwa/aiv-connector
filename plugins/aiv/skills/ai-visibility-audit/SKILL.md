---
name: ai-visibility-audit
description: Audit how ready a website is for AI assistants using the AIV connector, and turn the results into a prioritised fix list. Use when the user asks why their site is not cited by ChatGPT, Claude, Gemini or Perplexity, asks for an AI visibility, GEO or llms.txt audit, or wants to know which pages to improve first.
---

# AI visibility audit with AIV

AIV crawls the site sitemap and scores every URL 0-100 for AI readiness: a Markdown version of
the page, a canonical URL, JSON-LD structured data, a single H1, title and meta description.
It also serves an llms.txt file for the site and compares it with the sitemap.

## Steps

1. **Pick the site.** Call `list_sites`. If there are none, ask for the domain and call
   `add_site` (needs the changes permission), then `crawl_site`.
2. **Check freshness.** Call `get_site_overview`. If `last_crawled_at` is empty or older than a
   week, offer `crawl_site` and wait a minute or two before reading results again.
3. **Collect the weak spots.**
   - `list_urls` with `filter: low_score` for the lowest-scoring pages,
   - `list_urls` with `filter: missing_md` for pages without a Markdown version,
   - `list_urls` with `filter: errors` for broken URLs.
4. **Look closer at the worst pages.** Call `get_url_audit` for up to five of them to see which
   checks fail. When the stored analysis is missing, `analyze_content` with the page `url`
   gives the SEO, readability and GEO checks.
5. **Check llms.txt.** Call `get_llms_txt`. Note pages that matter but are not listed, and
   `missing_in_llms` from the overview when the site has its own llms.txt.

## Report

Give the user a short report:

- the average score and how many URLs have a Markdown version,
- the top issues grouped by type (for example "12 product pages have no JSON-LD"),
- a prioritised list of at most 10 actions, most impact first, each naming the URLs it covers,
- which actions AIV can do from the chat (create or generate Markdown pages and publish them,
  see the publish-llm-pages skill) and which need changes on the website itself.

Link the panel (`panel_url` from the overview) for details. Keep numbers exact; do not invent
scores for pages that were not crawled.
