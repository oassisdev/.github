## oassis — web infrastructure for AI agents

Search the web, extract pages and documents, crawl sites, and interact with a persistent
browser through an HTTP API or MCP. Use individual **Web Tools**, asynchronous **Tasks**,
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

### Three product layers

| Layer | Routes | What it does |
| --- | --- | --- |
| **Web Tools** | `/web/v1/scrape`, `/web/v1/map`, `/web/v1/search`, `/web/v1/session`, `/web/v1/act`, `/web/v1/feedback` | Read pages or documents, discover URLs, search, and operate a browser. |
| **Extraction Tasks** | `/tasks/v1/scrape/batch`, `/tasks/v1/crawl` | Start an asynchronous job, poll `GET /{id}`, or stop pending work with `POST /{id}/cancel`. |
| **Research Tasks** | `/tasks/v1/research` | Answer a research question from public pages with sources, progress and billing. Read `GET /{task_id}` or stop with `POST /{task_id}/cancel`. |
| **Scheduled Agents** | `/agents/v1` | Configure `price-watch`, `web-watch` or `competitor-monitor`, then read a service with `GET /agents/v1/services/{id}` or cancel it with `POST /agents/v1/services/{id}/cancel`. Currently free with an account key; HTTP only, no MCP tools. |

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
