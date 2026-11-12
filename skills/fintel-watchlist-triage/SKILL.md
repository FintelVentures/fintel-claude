---
name: fintel-watchlist-triage
description: Triage the user's Fintel stock lists. Use when asked to review a watchlist, what changed across my lists, or which names on a list need attention.
---

# Watchlist triage

Requires the user's signed-in Fintel account.

1. List the available lists with `fintel.list_stock_lists`, then read the chosen one with
   `fintel.get_stock_list` and `fintel.list_stock_list_items`. Confirm which list if several match.
2. Apply the same evidence funnel to every security using list-level tools such as
   `fintel.get_stock_list_filings`, `fintel.get_stock_list_insiders` and
   `fintel.get_stock_list_owners`.
3. Classify each item as **investigate now**, **monitor** or **no material change**, with the
   reason and the evidence date.

Triage is read-only. Adding or removing list items is a change: describe it and get confirmation.
Do not use broad outside web search for this workflow.

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
