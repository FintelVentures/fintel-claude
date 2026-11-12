---
name: fintel-insider-signal-review
description: Assess the strength of reported insider activity for one company, including transaction types, clusters, timing and alternative explanations. Use to interpret insider signals rather than merely retrieve trades.
---

# Insider signal review

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `insider_signal_review` / `insider-signal-review-v1`.

Call `fintel.get_security_insiders` with a bounded count. Preserve transaction classifications and transaction versus filing dates. Classify purchases and sales separately from grants, gifts, tax withholding, conversions and exercises. The code may be a description such as Purchase, TaxPay or OptionEx rather than a raw Form 4 letter; Purchase alone does not prove an open-market trade.

Explain the assessment, transactions, clustering across distinct people, alternative explanations, verification and coverage. Do not double count amendments or repeated rows. Roles, post-trade ownership, derivative status and trading plans remain unknown unless returned by cited evidence. Missing plan flags do not mean discretionary trading, and empty results do not prove nobody traded. Do not infer personal conviction or predictive accuracy.

Example: “How strong is the insider buying signal at ABC?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
