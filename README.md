# DataX France & EU Truth Engine — MCP Server (`stdio`)

Zero-dependency **Model Context Protocol (MCP)** `stdio` bridge (`Python 3.9+` standard library only — no `pip install` required) connecting AI agents (Claude Desktop, Cursor, OpenClaw, custom MCP clients) to live official **France & EU** registries with non-custodial pay-per-call settlement in **USDC** (Base, Polygon, Solana) and **MiCA EURC** (Base).

- **Live Endpoint:** `https://datax-fr.duckdns.org`
- **Machine Discovery:** [`/llms.txt`](https://datax-fr.duckdns.org/llms.txt) · [`/mcp.json`](https://datax-fr.duckdns.org/mcp.json) · [`/.well-known/agent-card.json`](https://datax-fr.duckdns.org/.well-known/agent-card.json) · [`/openapi.json`](https://datax-fr.duckdns.org/openapi.json) · [`/.well-known/ai-crawl-pricing.json`](https://datax-fr.duckdns.org/.well-known/ai-crawl-pricing.json)
- **Agent Payment Protocol & Wallet Guide:** See [`SKILL.md`](./SKILL.md)

---

## Official Data Sources Indexed

- **French Commercial Registry (`BODACC`):** Daily company formations (`CONSTITUCION` with capital), corporate modifications, deregistrations, and collective insolvency proceedings (`CONCURSO_DISOLUCION`). Legal entities (`pm` / 9-digit SIREN) only; natural persons (`pp`) skipped per GDPR.
- **French Public Procurement (`BOAMP`):** National, regional, and municipal calls (`PC`) and award notices (`PA`).
- **EU Registries:** **EU TED v3** procurement (`FRA`, `Sec TE`), **EU SEDIA** grants (`Sec EU`), and **EU Consolidated Financial Sanctions List (`FSF`, `Sec SF`)**.

---

## MCP Tools Exposed (7 Tools)

| Tool | Price (`USDC` / `EURC`) | Purpose |
| :--- | :---: | :--- |
| `get_pricing` | **Free** | Fetch supported networks, contracts, treasuries, and tier prices. |
| `get_catalog` | **Free** | Check live freshness (`data_version`) and record counts by section. |
| `search_tenders` | **`0.10`** | FTS5 BM25 + BI filter search across France & EU registries; returns opaque `item_ref` (`dx_...`). |
| `find_distressed_auctions` | **`0.10`** | Real-estate auction endpoint (populated on Spain node; empty on France-only DB). |
| `find_funded_companies` | **`0.10`** | Companies incorporated with capital in BODACC or winning EU/French awards. |
| `check_company_risk` | **`0.30`** | Screen 9-digit SIREN or company_name across BODACC insolvencies, EU FSF sanctions & awards. |
| `get_tender_detail` | **`0.50`** | Unlocks full verbatim record, winner corporate IDs, CPVs & official URLs from any `item_ref`. |

---

## Quick Setup (Claude Desktop / Cursor)

```json
{
  "mcpServers": {
    "datax-france-eu": {
      "command": "python3",
      "args": ["/absolute/path/to/mcp_bridge.py"],
      "env": {
        "DATAX_BASE_URL": "https://datax-fr.duckdns.org",
        "DATAX_TOKEN": "<unspent-utxo-token-from-issue-token>"
      }
    }
  }
}
```
