---
name: setup
description: First-run setup for the AIV connector. Checks the connection, shows the plan, and helps add and crawl the first website. Use right after installing AIV or when the user asks how to start with AIV.
---

# Set up AIV

1. Call `get_account`. If it fails with an authentication error, ask the user to connect AIV
   (sign in with their AIV account; creating one is free at https://aiv.piotrlitwa.com).
2. Tell the user their plan in one line. On a read-only plan, explain that reading the audit
   works, while adding sites and creating or publishing pages from the chat need the Own Key plan.
3. Call `list_sites`.
   - No sites: ask for the website domain, call `add_site`, then `crawl_site`.
   - One or more: show them with their average score and last crawl date.
4. Offer the next step: an AI visibility audit of the main site, or writing a first Markdown
   page for it.
