---
name: fintel-unusual-options-investigation
description: Investigate unusual options trades, sweeps, blocks or flagged volume anomalies for one security using supporting trades and flow context. Use to assess alternative explanations rather than an options overview or a trade recommendation.
---

# Unusual-options investigation

Contract: `unusual_options_investigation` / `unusual-options-investigation-v1` in the internal agent.
Resolve the listing with `fintel.search_securities`, then reuse the returned identifiers and name.
Inspect the live schemas and entitlement results. Public read-only research needs no private tools.

Choose an explicit bounded trade window, preserving the requested session/timezone and filters.
Call `fintel.get_security_unusual_option_flow`, `fintel.get_security_option_flow` and
`fintel.get_security_option_flow_summary` for the same window and compatible filters. Inspect
supporting rows and cursor/limit/truncation metadata. Unusual rows are flagged observations, not
necessarily the largest trades; preserve source ordering. Page when needed for the requested
scope and disclose any unexamined remainder. An excerpt's summed premium is not population premium.

For key observations show returned trade identifiers, execution time, contract/strike/expiry,
size, premium and units, bid/ask context, inferred direction and flag reason. Do not fabricate
missing fields, multipliers, correction status or historical baselines. Only calculate ratios
when numerator/denominator units and windows align, showing the inputs and formula. Missing
normal-volume history prevents a statistical claim that activity is unusual relative to normal.

Explain possible directional interest, hedging, closing trades, multi-leg activity and liquidity
as alternatives without asserting any intent or linkage not established by data. Sweeps alone do
not prove informed trading; volume above open interest does not establish new opening positions.
Use optional dated earnings-calendar, chain, IV or current-range evidence only when relevant.
Range timeout/unavailable states are gaps, not zero ranges. Premium/IV ranges are scenarios,
not confidence intervals or isolated earnings variance. Do not forecast a move from max pain.

Return the assessment, representative trades, same-window context, alternative explanations,
contrary evidence, unresolved questions, change conditions and coverage. If a required tool is
failed/denied, a full investigation is unavailable; report only the supported partial evidence.
An empty unusual-trade response is limited coverage and is not proof of no market activity.

## Research operating contract

Define the requested security/universe, horizon and benchmark; state unspecified or not
applicable rather than inventing them. Validate observation dates, units, financial periods,
coverage and conflicting sources before combining evidence. Show formulas, input lineage and
explicit assumptions for calculations. Keep observations, inferred signals and scenarios separate.
Return a conclusion with contrary evidence, unresolved questions and what would change the
assessment. Save or monitor only when requested, through the existing authorization and
confirmation controls; a research request does not authorize persistent changes.

Read [evaluation cases](references/evaluation-cases.md) when validating or releasing this workflow.
