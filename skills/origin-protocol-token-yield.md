---
name: origin-protocol-token-yield
description: Pull current and historical yield, ratios, collateral, and supply for an Origin yield-bearing token (OUSD, OETH, superOETHb, OS) from the Origin DeFi Analytics API.
generated: '2026-07-20'
method: generated
source: openapi/origin-protocol-openapi.json
api: Origin DeFi Analytics API
base_url: https://api.originprotocol.com
authentication: none (public read API)
operations:
  - getApiV2ByTokenAprTrailing
  - getApiV2ByTokenAprHistory
  - getApiV2ByTokenStatsByStat
  - getApiV2ByTokenRatios
  - getApiV2ByTokenCollaterals
  - getTotal-ousd
---

# Origin token yield lookup

Read yield and backing data for an Origin yield-bearing token. Token symbol is a
path parameter and must be one of `ousd`, `oeth`, `superoethb`, `os`. Add
`?chainId=` to select a chain (defaults to `1`, Ethereum mainnet). No auth required.

## Steps

1. **Trailing yield** — call `getApiV2ByTokenAprTrailing`
   (`GET /api/v2/{token}/apr/trailing`) for the current annualized APR/APY.
   Keep any `days` window at or below 100; larger windows may be unreliable.
2. **Yield history** — call `getApiV2ByTokenAprHistory`
   (`GET /api/v2/{token}/apr/history`) for the recent 30-day APR/APY plus the
   prior daily APY series.
3. **Point stats** — call `getApiV2ByTokenStatsByStat`
   (`GET /api/v2/{token}/stats/{stat}`) for a single metric such as
   `totalSupply`, `apy30`, `marketCapUSD`, `rebasingSupply`, or `yield`.
4. **Peg / credits ratio** — call `getApiV2ByTokenRatios`
   (`GET /api/v2/{token}/ratios`) for current and next credits-per-token.
5. **Backing** — call `getApiV2ByTokenCollaterals`
   (`GET /api/v2/{token}/collaterals`) to list backing assets and balances.
6. **Total supply** — call the scalar route (e.g. `getTotal-ousd`,
   `GET /total-ousd`) when you only need the plain supply number.

## Conventions & errors

- Responses are `application/json`; a few scalar totals return `text/plain`.
- Errors return `{ "error": "<message>" }` (not RFC 9457). A `404` means the
  token/record does not exist for that identifier or `chainId`; verify the symbol.
- This API is public and best-effort — cache results and do not use for
  mission-critical flows (per the provider). See
  `conventions/origin-protocol-conventions.yml` and
  `errors/origin-protocol-problem-types.yml`.
