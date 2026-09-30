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
