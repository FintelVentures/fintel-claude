---
name: fintel-options-positioning-review
description: Reconcile one stock's options flow, expiration positioning, implied volatility and gamma evidence. Use for options positioning around an event rather than one metric, a leaderboard or an execution strategy.
---

# Options positioning review

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `options_positioning_review` / `options-positioning-review-v1`.

Call all four required tools: `fintel.get_security_options_flow_sentiment`, `fintel.get_security_options_sentiment_by_expiration`, `fintel.get_security_implied_volatility` and `fintel.get_security_gamma_exposure`. Optional expiration analysis, positioning walls or current range may add context when available. Preserve quote/session/expiration dates and distinguish live, completed-session and end-of-day records.

Explain flow, positioning, volatility, gamma, counterevidence and coverage, matching sessions before interpreting agreement or disagreement. Direction is inferred; opening/closing, hedging and multi-leg intent may be unknown. Dealer gamma and walls depend on model assumptions, not known dealer books or guaranteed support/resistance. Do not infer who owns calls/puts, turn max pain into a forecast or promise price moves. Missing entitlements or strikes are gaps, not neutral signals.

Example: “What do ABC's options positions imply around earnings?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
