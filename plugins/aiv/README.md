# AIV - AI Visibility connector

Connect your [AIV](https://aiv.piotrlitwa.com) account to Claude, ChatGPT, Gemini CLI, Cursor,
VS Code and any other MCP client. AIV makes websites discoverable and citable by AI assistants:
it audits every sitemap URL for AI readiness, serves `llms.txt` for your site and hosts Markdown
pages written for LLMs. With the connector you review the audit, find the weakest pages, analyse
content for SEO and GEO, compare a page with the top 10 search results for a phrase, and create, AI-generate and publish Markdown pages without leaving the chat.

**Server URL:** `https://aiv.piotrlitwa.com/mcp/` (remote, Streamable HTTP, OAuth 2.1).
Nothing to install or run locally and no API key to copy: you sign in with your AIV account and
approve access. A free AIV account can read; adding sites and creating or publishing pages from
the chat is part of the Own Key plan.

This repository contains only the connector manifests, skills and documentation. The AIV service
itself runs at aiv.piotrlitwa.com.

## Install

| App | How |
|---|---|
| **Claude** (web, Desktop, mobile) | Customize → Connectors → **Add custom connector** → paste the server URL → Connect. |
| **Claude Code** | `/plugin marketplace add piotrlitwa/aiv-connector` then `/plugin install aiv@aiv` (connector + skills). Connector only: `claude mcp add --transport http aiv https://aiv.piotrlitwa.com/mcp/`, then `/mcp` → Authenticate. |
| **ChatGPT** | Settings → Apps & Connectors → Advanced → Developer mode → **Create**: paste the server URL, authentication OAuth. |
| **Codex CLI** | `codex mcp add aiv --url https://aiv.piotrlitwa.com/mcp/` then `codex mcp login aiv`. |
| **Gemini CLI** | `gemini extensions install https://github.com/piotrlitwa/aiv-connector`, then `/mcp auth aiv`. |
| **Cursor** | [Add to Cursor](https://cursor.com/en/install-mcp?name=aiv&config=eyJ1cmwiOiJodHRwczovL2Fpdi5waW90cmxpdHdhLmNvbS9tY3AvIn0%3D) |
| **VS Code** (Copilot) | [Install in VS Code](https://insiders.vscode.dev/redirect/mcp/install?name=aiv&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A//aiv.piotrlitwa.com/mcp/%22%7D) |
| **Other MCP clients** | Add a remote (Streamable HTTP) server with the URL above; OAuth is discovered automatically. |

The Gemini app on gemini.google.com does not accept custom connectors yet; use Gemini CLI.

## Tools

Read (free plan included): `list_sites`, `get_account`, `get_site_overview`, `list_urls`,
`get_url_audit`, `get_llms_txt`, `list_documents`, `get_document`, `analyze_content`,
`compare_with_top_results`, `search`, `fetch`.

Changes (Own Key plan): `add_site`, `crawl_site`, `create_document`, `generate_document`,
`update_document`, `publish_document`, `unpublish_document`. Clients ask you to confirm these.

## Skills (Claude and ChatGPT plugin)

- **ai-visibility-audit**: audit a site and get a prioritised fix list.
- **publish-llm-pages**: create, improve and publish Markdown pages and llms.txt entries.
- **seo-competitor-gap**: compare a page with the Google top 10 for a phrase and get a rewrite plan.
- **setup**: first-run check and adding your first site.

## Repository layout

```
.claude-plugin/marketplace.json   Claude Code plugin marketplace
plugins/aiv/                      the plugin (Claude + ChatGPT/Codex Agent Plugins format)
  .claude-plugin/plugin.json      Claude manifest
  .mcp.json                       MCP server for Claude
  plugin.json, mcp.json           portable Agent Plugins manifest (OpenAI)
  skills/                         skills
gemini-extension.json, GEMINI.md  Gemini CLI extension
server.json                       official MCP Registry entry
```

## Privacy and support

The connector reads and changes only the data of the AIV account you connect, and it does not
receive your conversations. [Privacy Policy](https://piotrlitwa.com/privacy.html) ·
[Terms](https://piotrlitwa.com/terms.html) · Disconnect any time at
[Connected apps](https://aiv.piotrlitwa.com/mcp/connect.php) ·
Support: piotr@piotrlitwa.com

## License

MIT for the contents of this repository (manifests, skills, docs). See [LICENSE](LICENSE).
