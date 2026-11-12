---
name: fintel-biotech-event-due-diligence
description: Assess trial evidence, success conditions and risks for a published biotech catalyst. Use for event due diligence rather than a calendar lookup, an invented pipeline or individual medical advice.
---

# Biotech event due diligence

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Resolve the listing with `fintel.search_securities` first, then reuse the returned country, symbol and company name. Ask for clarification if identity is ambiguous. This is public, read-only research; private account reads and mutations are unnecessary.

Required evidence failures must remain explicit coverage gaps. Empty data does not establish a positive or negative signal. Preserve source dates, units, currencies, missing values and truncation metadata. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. End with a concise coverage note and a relevant next verification step. Do not replace missing Fintel observations with model memory.

Contract: `biotech_event_due_diligence` / `biotech-event-due-diligence-v1`.

Call `fintel.get_security_biotech_catalysts`, then `fintel.get_biotech_catalyst` using the selected published event's returned ID whenever the catalog is nonempty. Do not guess IDs or skip detail retrieval. If no published event exists, report that coverage result rather than invent a pipeline. Confirm the selected company, asset, indication, phase, trial and event.

Explain the event, trial evidence, success conditions, risks, verification and coverage. Preserve tentative windows, precision and status instead of presenting estimated dates as firm. Distinguish endpoints, design, comparator, population and prior results from interpretation. Clinical milestones do not establish efficacy, regulatory approval, statistical significance or approval probabilities. Missing endpoint or trial-design detail remains a gap; do not translate this into individual patient advice.

Example: “What would support or weaken the thesis for ABC's next trial readout?”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
