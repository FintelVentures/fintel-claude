---
name: fintel-investment-thesis
description: Build an evidence-based investment thesis for one company with Fintel data. Use when asked for a thesis, a deep dive, 'is X a good investment', or the case for or against a stock.
---

# Investment thesis

## Output

1. **Thesis** in one or two sentences.
2. **Supporting evidence** and **contradicting evidence**, each with date and source tool.
3. **Catalysts** and **risks**, ranked by likely relevance.
4. **Key assumptions** and open **valuation questions**.
5. **Invalidation conditions**: specific, observable events that would make the thesis wrong.

## Evidence plan (bounded)

Resolve the security, then gather only what the thesis needs from: ownership
(`fintel.get_security_owners`), insiders (`fintel.get_security_insiders`), short interest
(`fintel.get_short_interest`), earnings and dividends (`fintel.get_security_earnings`,
`fintel.get_security_dividends`), analyst views (`fintel.get_security_analyst_ratings`,
`fintel.get_security_price_targets`) and rankings (`fintel.get_security_rankings`). Keep the call
count small; omit optional sources that are irrelevant and say so.

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
