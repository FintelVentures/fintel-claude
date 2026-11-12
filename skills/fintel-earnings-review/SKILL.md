---
name: fintel-earnings-review
description: Review a company's earnings with Fintel data. Use when asked about earnings results, a beat or miss, estimates versus actuals, guidance, or what changed this quarter.
---

# Earnings review

Require Fintel earnings history before anything else: call `fintel.get_security_earnings`. If it is
unavailable, stop and say so.

## Output

- Actual versus estimated results and the surprise, with the reporting period and date.
- Comparison with the prior period and the same period a year earlier where the data supports it.
- Guidance and margin changes only if the tools return them; otherwise state that they were not
  available rather than guessing.
- Why the surprise likely happened, labelled as interpretation.
- Unresolved questions to watch on the next report. Use `fintel.get_security_earnings_calendar` for
  the next date and `fintel.get_security_forecast` for forward estimates when available.

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
