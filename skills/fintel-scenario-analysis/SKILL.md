---
name: fintel-scenario-analysis
description: Frame conditional upside, base and downside outcomes for a company or event with a common horizon, explicit assumptions, triggers and invalidation conditions. Use for what-if analysis; use valuation-expectations or dilution-and-runway for their dedicated calculations.
---

# Scenario analysis

Scenarios are conditional frames, not forecasts. Avoid forecast language such as "will" or
"expect"; use "if... then".

## Output

For each of **upside**, **base** and **downside**: the assumptions, the trigger that would indicate
it is unfolding, and the invalidation condition. Where Fintel data supports it, quantify the
affected companies or levels (for example prices from `fintel.get_last_price`, estimates from
`fintel.get_security_forecast`). Add monitoring triggers: the dated events or data releases to
watch. Say clearly which numbers come from tools and which are the user's or your assumptions.

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
