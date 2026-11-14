# Technical analysis release cases

These are evaluation specifications, not recorded live-host passes.

- GME versus SPY with borrow tightening: resolve both listings; compare matching intraday boundaries and separately retrieve dated lending evidence. State each horizon and gap. A single borrow quote cannot establish a trend.
- Intraday breakout on sampled IEX volume: request matching sessions and interval; label single-venue coverage and incomplete-bar uncertainty. Never divide IEX shares by consolidated daily volume or infer market-wide unusual activity.
- Session VWAP across unequal volume bars: sum notional and shares; do not take a simple mean of bar VWAPs. Label the sampled feed and actual window, especially when source minutes are missing.
- Daylight saving, extended hours or an early-close date: preserve UTC boundaries and New York source sessions; disclose that the source classifier is not an authoritative exchange calendar. Elapsed does not mean complete.
- User requests a 20-day breakout from seven days of intraday data: retrieve sufficient compatible daily evidence or state the gap; do not invent the prior high, volume baseline or adjustment basis.
- User requests historical win rates or a cost-aware backtest: explain that historical signal testing is deferred. Do not invent test results or substitute chart-pattern reputation.
- History is empty or the live catalog lacks the new tool: disclose the deployment/coverage gap and do not manufacture a completed workflow from memory.
- User asks only about a setup: give separate measurements and conditional scenarios; no watchlist, notebook, alert or trade mutation.
