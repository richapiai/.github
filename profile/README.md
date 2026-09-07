<h1 align="center">RichAPI - GTM APIs for AI Native Teams</h1>

<p align="center"><b>One API key. Live GTM data. Pay only for results.</b></p>

<p align="center">
  <a href="https://app.richapi.ai"><b>Get an API key</b></a> ·
  <a href="https://richapi.ai">Website</a> ·
  <a href="https://mcp.richapi.ai/mcp">MCP server</a>
</p>

<p align="center">
  <img alt="endpoints" src="https://img.shields.io/badge/endpoints-~68-blue">
  <img alt="billing" src="https://img.shields.io/badge/billing-per%20successful%20result-brightgreen">
  <img alt="mcp" src="https://img.shields.io/badge/MCP-native-blueviolet">
  <img alt="credit price" src="https://img.shields.io/badge/1%20credit-%240.02-lightgrey">
</p>

---

Go-to-market data usually arrives one of two ways: a cached index you rent by the seat, or
five point tools with five bills and five failure points. RichAPI is neither.

It is **~68 endpoints behind one key** — person and company enrichment, people and lead
search, email finding and verification, phone finding, web and tech-stack intelligence,
B2B Social posts and activities, ad libraries, Maps, funding, traffic, and LLM enrichment —
**retrieved live at request time** and **billed only on a successful result**.

## See the billing rule, don't take our word for it

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="/assets/waterfall-dark.svg">
    <img width="900" alt="Terminal recording. A RichAPI email-finder call falls through provider one (412ms, no data) to provider two (291ms, hit), returns john.doe@acme.com and bills 5 credits. A second call tries both providers, finds nothing, and bills 0 credits." src="/assets/waterfall-light.svg">
  </picture>
</p>

Two calls. The first falls through to a second provider, returns an address, and bills
5 credits. The second finds nothing and bills **zero** — same endpoint, same waterfall,
no charge. That is the whole pricing model in fifteen seconds.

Run it against your own data:

```bash
curl -X POST https://api.richapi.ai/api/v1/email_finder \
  -H "x-api-key: $RICHAPI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"first_name":"John","last_name":"Doe","company_domain":"acme.com"}'
```

When nothing is found, you get a `200` — and you are charged nothing:

```json
{
  "success": false,
  "result": null,
  "providers_tried": 2,
  "execution_log": [
    { "provider": "…", "status": "no_data", "latency_ms": 412 },
    { "provider": "…", "status": "no_data", "latency_ms": 688 }
  ],
  "billed": false
}
```

That `execution_log` is the point. One call falls through an ordered chain of data
providers and stops at the first hit. You pay one flat price on a hit, zero on a miss, and
the receipt tells you who was asked, what each one said, and how long each took. No other
part of your stack shows you that.

## What lives in this org

| Repo | What it is |
|---|---|
| [**gtm-skills**](https://github.com/richapiai/gtm-skills) | 33 go-to-market skills for any agent that reads [`SKILL.md`](https://agentskills.io) — Claude Code, Cursor, Windsurf, Codex and 20+ others. It prices every run from a generated catalog and **refuses to spend a credit until you approve the total.** 11 of the 33 never spend at all. |
| [**n8n-nodes-richapi**](https://github.com/richapiai/n8n-nodes-richapi) | Community n8n node. Drop RichAPI endpoints into an n8n workflow without writing HTTP nodes by hand. *(publishing soon)* |
| **openapi** | The OpenAPI description of the public API, plus the generated Python and TypeScript SDKs. *(publishing soon)* |

## Why teams put this in production

- **Live beats cached.** Retrieval happens when you ask, not when someone last crawled. That
  also makes signal endpoints possible — everyone who commented on a competitor's post,
  a company's current employees, an active ad library — which no pre-built dataset can serve.
- **Outcome billing.** Only `2xx` is billed, per-result endpoints charge for what came back,
  and a waterfall miss returns `"billed": false`. No seats. No expiring monthly buckets. No
  contracts. Credits do not expire.
- **One key replaces the stack.** Enrichment, search, email, phone, verification, scraping,
  tech stack, ads, Maps, funding, traffic, YouTube, and LLM enrichment — one wallet, one
  integration, one place to debug.
- **Built for agents.** A hosted MCP server with no install and a catalog that updates itself:
  new endpoints show up inside your agents without you touching anything. Per-connection
  revocation included.
- **Throughput scales without a sales call.** Rate tiers rise automatically with spend,
  from 1 to 50 requests/sec.

## Start in about two minutes

1. Sign up at **[app.richapi.ai](https://app.richapi.ai)** — free credits, no card.
2. Create an API key and send it as the `x-api-key` header.
3. Call `POST https://api.richapi.ai/api/v1/enrich_profile` — 1 credit — or run the whole
   thing from an agent by pointing it at `https://mcp.richapi.ai/mcp`.

Browse and test every endpoint from the API Catalog in the dashboard before you write code.

## What RichAPI is not

Worth saying plainly, so you can rule us out fast:

- **Not a dataset you license.** There is no index to query offline and no bulk file to buy.
  If you need static coverage numbers to compare vendors, we will lose that comparison on
  purpose — ask us for a fresh-vs-cached diff on your own records instead.
- **Not a sender, a dialer, or a CRM.** We stop at the data. Your sequencer stays yours.
- **Not a seat-priced platform.** If you want per-user licensing and an annual contract, we
  are the wrong shape.

## Contributing

Issues and pull requests are welcome on any public repo here. Each repo carries its own
`CONTRIBUTING.md` and license — most are MIT. Security reports should go to the address in
that repo's `SECURITY.md` rather than a public issue.

---

<p align="center">
  <sub>Built by the team behind TexAu's automation engine — the same data plane, unbundled and sold as an API.</sub>
</p>
