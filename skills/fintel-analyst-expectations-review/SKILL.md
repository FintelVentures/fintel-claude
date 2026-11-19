---
name: fintel-analyst-expectations-review
description: Reconcile analyst price targets, rating distributions, fiscal-period forecasts and estimate dispersion for one stock. Use for consensus and disagreement analysis; use retained revision tools for comparable historical consensus and fiscal-target revision windows when available.
---

Use Fintel’s authenticated MCP tools for this public-data research workflow. Inspect tool availability and entitlement results before analysis. If required tools fail or are unavailable, explain the missing coverage; do not replace them with model memory. Successful empty results support only limited coverage claims. Use public research tools for this task; private account reads and mutations are unnecessary.

Contract: `analyst_expectations_review` / `analyst-expectations-review-v1`.

Resolve the listing with `fintel.search_securities`, then retrieve `fintel.get_security_price_targets`, `fintel.get_security_analyst_ratings`, `fintel.get_security_forecast` and `fintel.get_security_analyst_estimates`.

Explain consensus, target dispersion, rating distributions, forecast growth, analyst coverage, contradictory evidence and limitations. Preserve the source listing when secondary listings resolve to a primary listing. Distinguish forecast fiscal period, rating period, target record/update date and retained estimate receipt date; missing snapshot evidence remains unknown. Preserve fiscal/calendar reconciliation and quarantine statuses rather than inferring issuer period ends from provider dates.

Targets are opinions, not fair values or guaranteed returns. Do not invent target horizons, currency or counts. Annual and quarterly estimates or incompatible EPS accounting bases cannot be compared directly. Rating-count changes do not establish estimate revisions. Use `fintel.get_security_analyst_estimate_revisions` for retained provider-date-target history, checking the live schema and matching metric, period, currency and EPS basis. For explicit fiscal-target comparisons use `fintel.get_security_estimate_revision_signals` (US common/ADR listings) for 7/30/90-day receipt windows. `fintel.get_estimate_revision_rankings` selects one window, metric, frequency and direction across the covered current US company universe. These are endpoint comparisons, not a continuous history of analyst actions or provider revision times. Preserve target identity, baseline age, coverage/exclusions and unknown currency/accounting basis; nonpositive baselines cannot support ranked percentage changes. Analyst counts/dispersion do not identify individual analysts.

Use `fintel.get_watchlist_estimate_revision_rankings` only for an explicitly requested owned personal list, with its returned ID. This is a private read and does not establish historical list membership. A public analyst assessment does not require private lists.

Example: “How optimistic is analyst consensus for US:ABC, and where do analysts disagree?”

Write in the user’s language. Cite material observations with their source dates and clearly identify missing metadata. Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
