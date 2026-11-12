---
name: fintel-bull-bear
description: Stress-test a stock thesis with the strongest supported bull and bear cases, shared assumptions, conflicting evidence and observations that would settle disagreements. Use when the user requests both sides or challenges an existing view.
---

# Bull and bear review

Do not start from a predetermined conclusion.

## Output

1. The strongest **bull case** the evidence supports.
2. The strongest **bear case** the evidence supports.
3. **Shared assumptions** both sides rely on, challenged.
4. **Contradictions** in the evidence (for example insider selling against rising analyst targets).
5. **What would settle each dispute**: the specific data or event.

Draw evidence from ownership, insider activity, short interest, earnings, analyst data and
rankings via the Fintel tools. If the user asks which side you favor, apply the opinion rule in the
conventions: state a provisional preference and the fact that could flip it.

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
