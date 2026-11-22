---
name: fintel-options-positioning-review
description: Reconcile one stock's options flow, expiration positioning, implied volatility and gamma evidence. Use for an options market briefing or event positioning; use unusual-options-investigation to investigate individual flagged trades.
---

# Options positioning review

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `options_positioning_review` / `options-positioning-review-v1`.

Call all four required tools: `fintel.get_security_options_flow_sentiment`, `fintel.get_security_options_sentiment_by_expiration`, `fintel.get_security_implied_volatility` and `fintel.get_security_gamma_exposure`. Optional expiration analysis, positioning walls or current range may add context when available. Expiration analysis defaults to session and expiration-bucket totals. Request `include_detail=true` for entitled 0DTE intraday flow, strikes and the expiration heatmap. Preserve quote/session/expiration dates and distinguish live, completed-session and end-of-day records.

Check coverage and timestamps first, then select optional positioning, flow or volatility detail according to the user's question. Explain flow, positioning, volatility, gamma, counterevidence and coverage, matching sessions before interpreting agreement or disagreement.

Require gamma units, formula, multiplier, dollar scaling, move size and position-sign assumptions before interpreting exposure or walls; modeled open-interest exposure is not observed dealer inventory. Require quote quality and construction metadata before interpreting IV surfaces. Keep close/last-trade prices, EOD quotes, nominal 15:45 Greeks/spot and session volume/open interest separate. Check chain selection bounds, omitted counts and pagination before treating contracts as the universe. Inspect per-field IV-history dates, age and carry-forward provenance; repeated values alone do not prove a bug or freshness.

Treat put-heavy activity, max pain and unusual trades as evidence to investigate, never standalone directional predictions. Direction is inferred; opening/closing, hedging and multi-leg intent may be unknown. Dealer gamma and walls depend on model assumptions, not known dealer books or guaranteed support/resistance. Do not infer who owns calls/puts, turn max pain into a forecast or promise price moves. Missing entitlements or strikes are gaps, not neutral signals.

Example: “What do ABC's options positions imply around earnings?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

For an options briefing, summarize flow, positioning, volatility and expiry concentration first.
Preserve the required gamma read as explicitly modeled context. Relevant optional current/forecast
ranges must retain construction, input/expiry dates and errors; timeout/unavailable is not a zero
range or a neutral signal. Never present premium/IV ranges as probabilities or confidence intervals.

For volatility questions, the IV summary includes `research.expirationSummary` (ATM IV, 25-delta put-minus-call skew and straddle-implied moves) and `research.termStructureShape`. Distinguish an inverted front pair from a mixed or fully backwardated curve. Use `include_detail=true` for contract inputs. For earnings questions, opt into `include_earnings=true` and bound prior reports with `earnings_limit` (1–40, default 8). Preserve missing reactions, sample counts and snapshot-relative event inclusion. The full-expiry straddle premium and historical first-session earnings reaction have different horizons; their comparison is descriptive context, not earnings-isolated variance, a forecast or a historical implied-versus-realized backtest. An unavailable optional earnings comparison is a coverage gap even when IV succeeds.

Use gamma `exposure_analysis` for the spot-repriced flip, delta/vanna/calendar-time charm and quote-date 0DTE gamma. Keep provider gamma separate from model scenarios, call-long/put-short totals separate from all-options-long totals, and preserve model rates/dividends, timing assumptions and excluded-input coverage. A missing bounded scan crossing does not establish that no flip exists. For broad sentiment, use `fintel.get_market_options_context` and pair actual dates with `fintel.get_market_breadth` for US. Preserve market-universe gaps, SPY/QQQ ETF versus SPX cash-index distinctions, and the difference between the VIX/VIX3M index curve and monthly VX futures settlements.
