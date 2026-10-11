## oassis — the web, for agents that pay for themselves

**Web scraping, crawling and browser control** as an API and as an **MCP server**. Scrape any
page or document to markdown, map and crawl whole sites, and drive a real browser.

**Pay per call with a wallet. No API key, no signup, no monthly plan.** Your agent answers a
402 and the call runs.

```bash
curl -X POST https://api.oassis.dev/web/v1/scrape \
  -H 'content-type: application/json' \
  -d '{"url":"https://example.com","formats":["markdown","controls"]}'
```

That answers `402` with the exact price of that call. Pay it (x402, USDC on Base) and repeat.

### What it does that a scraper usually does not

- **A map of the controls** — every link, button and field with its role, its readable name
  and where it sits on screen. The map an agent needs to decide what to click.
- **Browser sessions that stay open** — look, click, look again, without losing state.
- **Documents by url** — PDF, Word, Excel and CSV come back as markdown, no browser involved.
- **Every output in one call** — markdown, html, links, controls, accessibility tree,
  elements by selector, screenshot, PDF, or AI-extracted JSON.

### Where to start

| | |
| --- | --- |
| Site | **[oassis.dev](https://oassis.dev)** |
| MCP server | `https://api.oassis.dev/mcp` — listed as `dev.oassis/scraper-crawler` |
| Code | [oassis-api](https://github.com/oassisdev/oassis-api) |
| OpenAPI | [api.oassis.dev/openapi.json](https://api.oassis.dev/openapi.json) |
| For models | [api.oassis.dev/llms.txt](https://api.oassis.dev/llms.txt) |

Prices start at **$0.001** a page. Quoted before the work, refunded when the work does not
happen, and the balance never expires.

### Agent tasks

Ask a question in plain words and get an answer with its sources. The agent plans its own steps,
reads public pages and answers. `POST /agent/v1/tasks` with an API key and a balance; the budget is
reserved first and the unused part comes back. Read it with `GET /agent/v1/tasks/{id}`, stop it with
`POST /agent/v1/tasks/{id}/cancel`. Also available as the MCP tools `web_task_start`, `web_task_status`
and `web_task_cancel`. Details in the [code repository](https://github.com/oassisdev/oassis-api#agent-tasks).
