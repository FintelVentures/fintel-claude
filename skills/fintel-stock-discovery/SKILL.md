---
name: fintel-stock-discovery
description: Find research candidates from Fintel leaderboards and rankings, including squeeze candidates, yield leaders and market movers. Use for ranked shortlists; use screen-builder to design custom criteria and specialist assessments to investigate one returned stock.
---

# Stock discovery

Present Fintel leaderboards and rankings as research shortlists, not recommendations to buy.

## Workflow

1. Start from the catalog: `fintel.list_leaderboards` and `fintel.list_rankings`. If the user named a
   general ranking (short squeeze, dividend yield, market cap, short interest, volume, gainers,
   losers) open that board directly with `fintel.get_leaderboard` or its dedicated tool such as
   `fintel.get_short_squeeze_leaderboard`. Otherwise propose the best-fit board and ask.
2. Return the entries with rank, ticker, the Fintel `name`, and the ranking value, plus the board's
   as-of date and universe.
3. Do not enrich every row. After presenting the board, ask which returned security merits deeper
   research. A reply such as a ticker, a company name or "the second one" selects it.

If the user wants private picks tailored to them, first confirm their goals and constraints
(horizon, risk tolerance, sectors to avoid) before narrowing the list.

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
