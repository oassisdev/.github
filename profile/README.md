## oassis — web infrastructure for AI agents

Search the web, extract pages and documents, crawl sites, and interact with a persistent
browser through an HTTP API or MCP. Use individual **Web Tools**, asynchronous **Web Tasks**,
or scheduled **Agents** for monitoring.

### Access and credits

- **MCP without an API key:** a one-time **100-credit trial for scrape and map**.
- **API key:** the same account credits work over MCP and HTTP. Verified accounts receive
  **1,000 welcome credits once**. Generate your key in the [billing dashboard](https://oassis.dev/dashboard/billing).
- **1 credit = $0.002.** A basic single-format page costs 1 credit. Other formats, browser
  time, actions and research are charged according to the requested work; fractional credits are supported.
- Packages: **2,500 / 10,000 / 25,000 credits for $5 / $20 / $50**, once or monthly.
  The dashboard shows checkout availability.
- **x402:** paid HTTP Web Tools and Task starts also accept independent wallet payment
  in USDC on Base, without an account. An unpaid request returns a **402 quote**, not a payment.
- Eligible unused work is refunded to account credits. **Settled x402 payments have no
  automatic on-chain refund.**

### Web Tools

| MCP tool | HTTP route | What it does |
| --- | --- | --- |
| `web_scrape` | `POST /web/v1/scrape` | Read a page or document in the requested formats. |
| `web_map` | `POST /web/v1/map` | List a site's URLs from its sitemap and optionally the page. |
| `web_search_exa` | `POST /web/v1/search` | Search the web. |
| `web_session_open` | `POST /web/v1/session` | Open a browser session and inspect its controls. |
| `web_act` | `POST /web/v1/act` | Interact with an open browser session. |
| `web_session_close` | `POST /web/v1/session/{id}/close` | Close the browser session and settle any outstanding time. |
| `web_feedback` | `POST /web/v1/feedback` | Report whether a result was correct. Free. |

### Web Tasks

| MCP tool | HTTP route | What it does |
| --- | --- | --- |
| `web_scrape_batch` | `POST /tasks/v1/scrape/batch` | Start a batch extraction job from a supplied list of URLs. |
| `web_batch_status` | `GET /tasks/v1/scrape/batch/{id}` | Read batch status and collect its results. |
| `web_batch_status` | `POST /tasks/v1/scrape/batch/{id}/cancel` | Cancel pending batch work. With MCP, send cancel: true. |
| `web_crawl` | `POST /tasks/v1/crawl` | Start a crawl job that discovers and reads linked pages. |
| `web_crawl_status` | `GET /tasks/v1/crawl/{id}` | Read crawl status and collect its results. |
| `web_crawl_status` | `POST /tasks/v1/crawl/{id}/cancel` | Cancel pending crawl work. With MCP, send cancel: true. |
| `web_task_start` | `POST /tasks/v1/research` | Start research from public pages and return an answer with sources. |
| `web_task_status` | `GET /tasks/v1/research/{id}` | Read research progress, sources, result and billing. |
| `web_task_cancel` | `POST /tasks/v1/research/{id}/cancel` | Cancel pending research work. |

### Agents

Scheduled monitoring is separate from Web Tasks. Configure `price-watch`, `web-watch` or
`competitor-monitor` under `/agents/v1`. Read a report with
`GET /agents/v1/services/{id}`; stop a service with
`POST /agents/v1/services/{id}/cancel`. Currently free with an account key; HTTP only.
Account credits are separate from Web Tools: `GET /web/v1/account` requires an API key.

Close a browser session explicitly with **`POST /web/v1/session/{id}/close`**.
The corresponding MCP tool remains **`web_session_close`**. Closing has no extra fee;
outstanding browser time is settled when applicable. The previous DELETE route is retired.

A successful Task start confirms acceptance, not completion. Poll the result; research can
finish with a partial answer. API-key research reserves a maximum budget and settles actual
cost. HTTP/x402 research purchases a fixed execution budget; retain the returned `access_token`
and send it as `Task-Token` for status and cancellation.

### Try the HTTP quote

```bash
curl -i -X POST https://api.oassis.dev/web/v1/scrape \
  -H 'content-type: application/json' \
  -d '{"url":"https://example.com","formats":["markdown"]}'
```

Without credentials this returns **HTTP 402** with the price in `PAYMENT-REQUIRED`.
Use an API key and credits, or complete the x402 payment and repeat the request.

### Where to start

| Resource | Link |
| --- | --- |
| Website | [oassis.dev](https://oassis.dev/) |
| Create an account | [oassis.dev/signup](https://oassis.dev/signup) |
| API keys and credits | [Billing dashboard](https://oassis.dev/dashboard/billing) |
| MCP server and tool catalog | [api.oassis.dev/mcp](https://api.oassis.dev/mcp) |
| OpenAPI | [api.oassis.dev/openapi.json](https://api.oassis.dev/openapi.json) |
| For models | [api.oassis.dev/llms.txt](https://api.oassis.dev/llms.txt) |
| Source code | [oassis-api](https://github.com/oassisdev/oassis-api) |
