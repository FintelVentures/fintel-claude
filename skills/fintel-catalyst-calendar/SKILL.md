---
name: fintel-catalyst-calendar
description: List upcoming dated catalysts for a company from Fintel data. Use when asked what is coming up, upcoming earnings or dividend dates, ex-dividend dates, or events to watch.
---

# Catalyst calendar

Resolve one security, then require its canonical calendars:
`fintel.get_security_earnings_calendar` and `fintel.get_security_dividend_calendar`. Biotech names
may also have `fintel.list_biotech_catalysts`.

## Output

A dated list, soonest first, each item with the event, the date, whether the date is confirmed or
estimated, and why it matters. Preserve date uncertainty; never present an estimated date as firm.
Rank by likely relevance and note anything you could not check.

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
