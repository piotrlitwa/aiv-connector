---
name: seo-competitor-gap
description: Compare a page with the pages ranking in the top 10 for a search phrase using the AIV connector, and turn the differences into a concrete rewrite plan (headings, length, title, structured data). Use when the user asks why competitors rank higher, how to beat the top results for a phrase, or how to restructure a page for a keyword.
---

# Competitor gap analysis with AIV

`compare_with_top_results` analyses the pages ranking for a phrase with the same parser AIV uses
for its audit and compares them with the user's page: title, meta description, H1-H3 structure,
heading topics, word count, paragraphs, links, images, dates and structured data.

## Steps

1. **Agree on the phrase and the page.** One phrase per comparison, in the language people
   search in. The page must be on a site in the AIV account (`list_sites`).
2. **Get the top results.** If you can search the web, search the phrase and pass the organic
   results (no ads, no video or map blocks, best first, up to 10) as `competitor_urls`. Otherwise
   leave `competitor_urls` empty; AIV fetches the Google top 10 when its search is configured.
3. **Run** `compare_with_top_results` with `site`, `url` and `keyphrase`. Each analysed page counts
   towards the plan quota; `get_account` shows what is left.
4. **Read the result.** `gaps` is ordered by impact. `heading_topics_missing` lists topics that
   several top pages cover in their H2/H3 and the page does not, with example headings: group
   them into real subtopics (the matching is by word stem, so judge the meaning yourself).

## Report

- Two or three sentences on where the page stands against the median of the top results.
- A rewrite plan: a proposed title and H1 with the phrase, then an H2/H3 outline that adds the
  missing subtopics in a sensible order, a target length close to the median, and the
  structured data to add (for example FAQPage when most top pages use it).
- Quick wins first (title, H1, meta description, first paragraph), larger content work after.
- Say plainly that this compares on-page structure only; rankings also depend on links,
  authority and search intent.

If the account has the Own Key plan, offer to draft the improved page in Content Studio with
`create_document` or `generate_document` and to publish it after the user approves.
