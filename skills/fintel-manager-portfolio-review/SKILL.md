---
name: fintel-manager-portfolio-review
description: Compare one investment manager's latest two disclosed 13F portfolios using amendment-aware changes and concentration evidence. Use for a public manager portfolio; this does not read the user's private portfolio or establish current trades or performance.
---

Use Fintel’s authenticated MCP tools for this public-data research workflow. Inspect tool availability and entitlement results before analysis. If required tools fail or are unavailable, explain the missing coverage; do not replace them with model memory. Successful empty results support only limited coverage claims. Use public research tools for this task; private account reads and mutations are unnecessary.

Contract: `manager_portfolio_review` / `manager-portfolio-review-v1`.

Call `fintel.search_managers` with the supplied manager name or slug. Select exactly one returned identity; if ambiguous, ask which manager. Use its integer `managerId` with `fintel.get_manager_portfolio_changes`.

Explain report periods and amendment provenance, newly/no-longer-disclosed lines, supported share increases/reductions, disclosed concentration, counterevidence and coverage. Respect `comparisonAvailable`, period truncation, ambiguous identifiers, complete-value flags and the top-50 position excerpt. Complete comparisons require complete ingested snapshots; absence from an excerpt does not establish an exit.

New disclosure is not proof of a new purchase; no-longer-disclosed is not proof of a sale. Preserve security class, put/call, units and source multipliers. Separate share changes from market-value effects. Identifier changes, confidential holdings, corporate actions and reporting exclusions may affect comparisons. Delayed 13F long-position disclosures do not establish current holdings, intent, performance or a complete portfolio.

Reported values are normalized dollars. Missing multipliers mean one, matching OwnerTransaction baked accessors; preserve record-specific normalization for historical filings and do not apply a blanket extra conversion by 1,000.

Example: “What changed in Alpha Manager’s latest disclosed portfolio?”

Write in the user’s language. Cite material observations with their source dates and clearly identify missing metadata. Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
