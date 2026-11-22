# Financial statements, valuation and price evidence

Use `fintel.get_security_financial_statement` for a resolved listing, selecting `kind=income`,
`balance` or `cash_flow` and an explicit period. Default source is `capital_iq`; request
`source=sec` for retained US filing evidence. Do not silently combine sources or fill withheld
SEC metrics from another filing/provider. The tool defaults to four period summaries. Set
`include_evidence=true` with a small `limit` when the question requires per-metric filing and
derivation receipts.

SEC supports annual/quarterly statements and TTM additive income/cash-flow projections. Inspect
per-metric evidence, missing/conflicting lines, filing cohorts and revision reconciliation.
Quarters follow observed fiscal boundaries; compatible YTD subtraction needs the returned
same-filing proof. When present, `asFiledDifferences` shows fiscal Q4 estimates calculated from
the original annual 10-K and nine-month 10-Q. Cite both filings and preserve the unverified
revision status. Keep these estimates out of ratios and TTM. TTM needs four contiguous reconciled
quarters: never sum balances, EPS or
weighted shares. FCF is CFO minus reported PP&E payments, preserving signs. Returned margins are
fractions and dividend coverage is a multiple; use positive denominators, compatible currencies
and joint revision evidence. A withheld ratio remains unavailable. Company Facts lacks original
XBRL contexts/dimensions and does not reconstruct historical public knowledge.

For `capital_iq`, preserve `meta.audit`, typed periods and warnings. Provider standalone quarters
can be used without subtracting adjacent quarters. Unverified duration values in `reportedValues`
are withheld from standardized values and cannot support quarter comparisons or runway.
Balance-sheet instants remain distinct from cash-flow durations. Retrieval time is not publication.

`fintel.get_sec_financial_facts` takes an issuer CIK and optional exact taxonomy/concept/unit,
accession and period filters. Obtain the CIK from returned identity evidence, never guess it.
These are unmapped reported observations, not canonical statements. Follow `meta.next_args` to
retain the capture and source ordinal. `known_at` requires both collection and index publication
by cutoff; latest indexed capture may precede a newer unindexed collection. Preserve that warning.
Explicit capture IDs stay pinned. Retention cutoffs are not historical public-availability claims.

For market cap/EV use `fintel.get_security_data_point` with exact dictionary keys. Preserve exact
values, financial/quote dates and `filing_provenance`, including share/ADR/FX evidence and
`availability_fallback`. A retained baseline awaiting evidence retains its original effective
date; it is not a newly verified quote or a current market cap. Null values and failed valuation
validation must not be reconstructed from diagnostic components. These estimates are not certified
for publication-time backtests.

`fintel.get_last_price` returns a retained trade or EOD fallback, not a feed heartbeat. Preserve
`is_eod_fallback`, `as_of`, `as_of_date`, `freshness_class` and `freshness_status`. EOD fallback has
no trade timestamp and does not itself mean stale. `is_quote_stale` is deprecated/null. For close
comparisons use `last_eod_close` with `last_eod_close_date`, or date-matched bars. `previous_close`
is strictly before the retained trade's market date (or fallback date), not necessarily the newest
EOD bar. Range and volume can be unavailable when the retained trade predates newer bars; never
combine dates silently. A requested session does not establish an observed session.

For DCF, `fintel.calculate_research_scenario` supports `kind=discounted_cash_flow` with explicit
`currency`, `forecastCashFlows`, `discountRate`, `terminalGrowthRate`, `netDebt`, `otherClaims`
and `sharesOutstanding`. Follow live constraints: annual year-end unlevered FCFF, matching scales,
positive terminal cash flow and discount rate above terminal growth. CFO minus capex is not
automatically FCFF. Forecasts and discount rates are assumptions, not observed facts; explicit zero
claims differ from omitted claims. There is no automatic forecast construction or FX conversion.

Evaluation cases:
- SEC TTM has one unreconciled quarter: report missing evidence; do not sum mixed filings or EPS.
- A market cap carries a retained baseline: retain its original date and pending-evidence status.
- EOD fallback after a missing trade: show closing date, unknown freshness and no invented timestamp.
- Screen price differs from a retained trade: compare date-matched daily closes before alleging an error.
