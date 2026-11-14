---
name: fintel-earnings-review
description: Review reported earnings results, actual versus estimated figures, supported period comparisons and open questions. Use after results; use earnings-preview before an announcement and earnings-quality-review for profit-to-cash analysis.
---

# Earnings review

Resolve the listing with `fintel.search_securities` and reuse its returned identifiers/name.
Require Fintel earnings history before analyzing results: call `fintel.get_security_earnings`. If it is
unavailable, stop and say so.

## Output

- Actual versus estimated results and the surprise, with the reporting period and date.
- Comparison with the prior period and the same period a year earlier where the data supports it.
- Guidance and margin changes only if the tools return them; otherwise state that they were not
  available rather than guessing.
- Why the surprise likely happened, labelled as interpretation.
- Unresolved questions to watch on the next report. Use `fintel.get_security_earnings_calendar` for
  the next date and `fintel.get_security_analyst_estimates` for period-specific forward estimates
  when available. `fintel.get_security_earnings_surprises` and
  `fintel.get_security_earnings_price_drift` can add historical context. Preserve EPS basis and
  currency; exact calendar-day reactions are not trading-session moves. Use earnings-preview for
  a pre-announcement briefing and earnings-quality-review for cash conversion analysis.

## Conventions (all Fintel skills)

- Use the Fintel connector for market data, never memory. Call only the tools you need and report
  the as-of date or period the tools return.
- Use the company `name` returned by Fintel. Never infer a company name from a ticker.
- Fail closed: if a tool this workflow requires is unavailable or returns nothing, say what is
  missing and what you could not assess. Do not substitute outside web research or invent figures.
- Finish with a short coverage note (examined, unavailable, stale), then ONE bounded next step that
  names its subject, for example "Want me to run an earnings review on NVDA?" A plain "yes" then
  resumes that action.
- If asked which option you prefer, answer directly: state the preference first, then the criteria,
  the key assumption, and what would change it. Name the missing fact if evidence is incomplete.
  Do not refuse with boilerplate such as "I can't give recommendations".
- Analysis is not authorization. Never create, change or delete anything in the user's Fintel
  account (stock lists, alerts, notebooks, team content) without describing the change and getting
  explicit confirmation first. Read-only lookups need none.
- This is research support, not personalized investment advice.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

Read [evaluation cases](references/evaluation-cases.md) when validating or releasing this workflow.

Fiscal labels that conflict across source rows remain unknown; preserve source_lineage and do
not assign a guessed year. Compare actuals with estimates retained for the same event, period,
currency and accounting basis. Current forward consensus is not the pre-announcement expectation.
If expectations are unavailable, withhold a beat/miss calculation; percentage surprises require
a positive nonzero expected denominator and visible inputs. Event-study benchmark differences
are not beta-adjusted alpha or proof of earnings causality.
