# Macro series through Fintel MCP

Use the general source/series interface. The live catalog is authoritative; initially `source=fred`
covers 120 collected series. Discovery is independent of whether observations are retained or fresh.

- `fintel.list_macro_series`: search `query` over native IDs, titles, descriptions and aliases;
  optional source, page and limit. Filters apply before stable ID pagination. Search `risk free rate`
  or `WACC` to find DGS10, `consumer price` for price indexes, or the exact native ID.
- `fintel.get_macro_series` with `source` and `series_id`: inspect units, seasonal adjustment,
  frequency, original source, citation, terms, available dates and import health.
- `fintel.get_macro_observations` with the same identity: default `limit=1`, `order=desc`, end UTC
  today. Optional inclusive `start_date` / `end_date` use YYYY-MM-DD. For history, increase limit
  (normally up to 250) and use returned `meta.next_args` unchanged for subsequent pages.

Example: `{"source":"fred","series_id":"DGS10","end_date":"2026-11-13","limit":1}`.
Use the actual returned date, which can precede the requested cutoff. An explicit missing source
cell stays unavailable; do not silently skip it, fill it, or turn it into zero. Native values and
`rate_decimal` are exact decimal strings or null. Zero and negative rates are valid observations.

`rate_decimal` is present only for explicitly typed interest-rate percentages: 4.25 percent becomes
0.0425. UNRATE is a percentage but is not an interest rate. CPI/PCE indexes are price levels, PAYEMS
is an employment level in thousands, and GDP levels may use annualized reporting conventions;
none of these is automatically a period change or growth rate. Preserve base years, seasonal
adjustment and scale. For FX, quote `fx_quote_currency` per one `fx_base_currency`; do not invert
silently. A trade-weighted currency index is not a bilateral FX rate.

For USD nominal cash flows, a dated nominal Treasury tenor can be an explicit risk-free proxy;
match currency, horizon and nominal/real basis. DFII yields are real. Treasury constant-maturity
quotes are not a bootstrapped zero curve. Breakevens include risk/liquidity premia. An observed
Treasury yield is neither WACC nor an equity risk premium. WACC additionally requires explicit
ERP, beta, cost of debt, tax rate and capital weights; a DCF also requires compatible cash flows,
growth/terminal assumptions and the enterprise-to-equity bridge.

Economic dates, first retention timestamps, last successful imports and response retrieval times
mean different things. These tools read latest retained values with revisions, not ALFRED vintages
or what was publicly known on a past date. Keyset paging is not an immutable snapshot; late inserts
or revisions may change later reads. Report collection overdue/failure flags and the per-frequency
observation-age warnings; do not call old monthly or quarterly data current daily observations.
Cite the original source and FRED using returned citation/source_url and preserve source terms.

Evaluation examples:
- Latest risk-free proxy: discover DGS10, show actual date and percent/decimal units; never label it WACC.
- Historical DCF cutoff: use end_date but disclose latest-retained revisions; list missing model assumptions.
- UNRATE / CPI / payrolls: no interest-rate conversion or invented growth transformations.
- DEXUSEU: report USD per EUR with full returned precision.
- Missing latest source cell: report unavailable with date; no automatic prior-value substitution.
- History: follow next_args; reject changed-filter cursors and preserve inclusive economic bounds.
