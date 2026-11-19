---
name: fintel-technical-analysis
description: Describe one US stock's intraday price-volume conditions, session VWAP and benchmark comparison using sampled IEX bars. Use for technical setups and conditional scenarios; historical signal testing and predictive pattern validation are not supported.
---

# Intraday technical analysis

Inspect the live Fintel tool catalog and resolve the stock and any benchmark with `fintel.search_securities`. Reuse each returned country/symbol. Intraday bars currently support US listings only. If a dependency is absent, denied or empty, identify that gap; do not invent bars or present the workflow as completed. This is read-only public research.

Call `fintel.get_intraday_bars` with ISO `startDate`/`endDate` spanning at most seven inclusive New York calendar dates, `intervalMinutes` of 1, 5, 15, 30 or 60, and an explicit `session` (`regular`, `premarket`, `afterhours`, `extended`, `all`). Prefer regular sessions unless the question concerns extended trading. Read the adjustment, session, missing-bar and completion metadata. Empty intervals are omitted, not filled. IEX volume is sampled single-venue volume: it cannot establish consolidated unusual volume and must not be divided by consolidated daily average volume. A partial-session volume comparison needs matching elapsed-session history from the same feed; otherwise report it unavailable.

Inspect `is_complete` and `interval_elapsed` separately. `is_complete=null` means unverified, even after an interval has elapsed; active intervals are false. Source sessions use New York time and timestamps use UTC. Regular buckets anchor at 09:30 and never cross source session/date boundaries. The source session classifier does not know holidays or early closes. Do not present its classifications as an authoritative exchange calendar.

For a benchmark comparison, retrieve bars for both listings with identical dates, session and interval. Compare only matching observed boundaries and compatible raw-price windows; do not shift dates or fill missing benchmark observations. Report each return and their percentage-point difference, and label the sampled venue and horizon. Raw intraday prices/shares are not split/dividend adjusted. Withhold cross-action comparisons unless compatible corporate-action evidence establishes the basis. `fintel.get_last_price` can provide separately timed quote context; it must not replace missing bars.

For session VWAP, sum returned `notional_volume` and divide by summed `volume_shares` from the requested session's start. Never average bar VWAPs without volume weights. Because empty minutes are omitted and ingestion completeness is unverified, describe this as VWAP of the returned IEX trades, not the full market's acquisition price. A multi-day or partial-session window must be labeled with its exact boundaries; it is not automatically a session VWAP or an event-anchored VWAP.

For daily context, `fintel.get_price_bars` supplies a separate daily dataset. Do not mix its adjusted price basis or consolidated volume with raw intraday samples. If a user requests a 20-day breakout, unusual consolidated volume or a technical indicator, use only compatible, sufficient returned inputs and state the formula and warm-up. Do not infer a 20-day setup from seven days of IEX history or claim provider-unverified adjustments are complete. No dedicated indicator or historical signal-testing tool is added by this workflow.

When borrow tightening is part of the question, call `fintel.get_borrow_rate` with its advertised history arguments. Compare dated rates and provider-specific available shares only when comparable observations exist; one current observation cannot establish tightening. Present borrow conditions separately from price, volume and benchmark measurements.

Show a compact measurement table with value, horizon/session, observation time, source and limitations, then explain which conditions support or weaken the setup. Describe conditional continuation/invalidation scenarios rather than asserting predictive value from a chart pattern. Preserve currency, adjustment rules, calculation version and evidence metadata. Underlying minutes are obtained by repeating the same query with `intervalMinutes=1`; later ingestion revisions may change them.

Historical signal testing, win rates, transaction-cost simulations, market breadth, volume profiles, arbitrary anchored VWAP and dedicated indicators remain unsupported by these new tools. Do not claim a pattern has been historically validated. Monitoring requires the user's explicit intent and discovery of supported alert definitions; technical research alone does not authorize an alert or trade.

Example: “How is GME trading this session relative to its IEX VWAP and SPY, and do dated borrow observations show tightening?”

Read [evaluation cases](references/evaluation-cases.md) when validating or releasing this workflow.

When using `fintel.get_last_price`, distinguish retained trades from `is_eod_fallback`. EOD
fallback has a closing date, not a trade timestamp; neither category proves live feed freshness.
Use `last_eod_close_date` for daily-close comparisons and `previous_close_date` for the daily-change
baseline. Preserve unknown session/freshness and missing range/volume; never combine a retained
older trade with newer daily bars as if they were one observation.
