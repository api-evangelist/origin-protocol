---
name: origin-protocol-protocol-revenue
description: Report Origin Protocol revenue, fees, product stats, and OGN buyback activity from the Origin DeFi Analytics API.
generated: '2026-07-20'
method: generated
source: openapi/origin-protocol-openapi.json
api: Origin DeFi Analytics API
base_url: https://api.originprotocol.com
authentication: none (public read API)
operations:
  - getApiV2ProtocolProtocol-fees
  - getApiV2ProtocolDaily_revenue
  - getApiV2ProtocolCumulative_revenue
  - getApiV2ProtocolProducts_stats
  - getApiV2OgnBuybacks
  - getApiV2OgnBuyback_stats
---

# Origin protocol revenue & OGN buybacks

Summarize protocol economics: revenue, fees, per-product stats, and the OGN
buyback program that recycles revenue. All read-only, no auth.

## Steps

1. **Revenue snapshot** — call `getApiV2ProtocolProtocol-fees`
   (`GET /api/v2/protocol/protocol-fees`) for revenue now vs. 1d/7d/30d/90d ago
   plus a daily history series.
2. **Daily & cumulative revenue** — call `getApiV2ProtocolDaily_revenue`
   (`GET /api/v2/protocol/daily_revenue`) and `getApiV2ProtocolCumulative_revenue`
   (`GET /api/v2/protocol/cumulative_revenue`) for trend and lifetime totals.
3. **Per-product breakdown** — call `getApiV2ProtocolProducts_stats`
   (`GET /api/v2/protocol/products_stats`) to attribute revenue/TVL across OETH,
   OUSD, OS, superOETHb, and ARM.
4. **OGN buybacks** — call `getApiV2OgnBuybacks`
   (`GET /api/v2/ogn/buybacks`) and `getApiV2OgnBuyback_stats`
   (`GET /api/v2/ogn/buyback_stats`) to show how revenue funds OGN buybacks.

## Conventions & errors

- Time-series endpoints accept `offset`/`limit` (and `days` where applicable).
- Dates in payloads are often unix timestamps/epochs.
- Errors return `{ "error": "<message>" }`; `503` means the upstream indexer is
  temporarily unavailable — retry with backoff. See
  `conventions/origin-protocol-conventions.yml`.
