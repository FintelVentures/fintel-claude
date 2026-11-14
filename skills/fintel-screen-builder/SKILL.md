---
name: fintel-screen-builder
description: Design, validate and execute custom stock screens with Fintel Workbench. Use for compound filters, formulas, rankings, historical screening, backtests and user-requested saved screens; use stock-discovery for existing leaderboard shortlists.
---

# Screen builder

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Start with `fintel.get_screening_capabilities` for the implemented language, function signatures, examples, workflow, limits and warnings. Universe screening does not require resolving an individual listing. If execution tools are absent from the connected host, explain the missing capability and label any proposed program as unexecuted; never invent matches.

Required evidence failures must remain explicit coverage gaps. Preserve returned units, currencies, missing values, dates and warnings. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. Do not replace missing Fintel observations with model memory.

Contract: `screen_builder` / `screen-builder-v2` (portable MCP workflow; does not change any separate server-side agent contract).

## Design and validation

1. Call `fintel.list_data_definitions`, respecting dictionary pagination, then `fintel.get_data_definition` for relevant returned keys. Never guess metric aliases or substitute unsupported historical or clustering conditions. A leaderboard shortlist is a different workflow.
2. Translate the objective into a complete semicolon-terminated Workbench program. Explain the universe, criteria, sorting, exclusions and missing-data policy. For each criterion preserve its exact key, operator, threshold and units; distinguish user-supplied thresholds from proposed assumptions. Ask a bounded clarification when an unresolved choice materially changes the criteria.
3. Follow the live capabilities for syntax and supported functions. Numeric scales vary by metric: the literal `5%` evaluates to `5`, not `0.05`. Named subqueries and dated aggregate sets are unsupported. Do not invent features.
4. Call `fintel.validate_screen` with `program`. Correct line/column diagnostics until `data.valid=true`; a validation success establishes syntax/access, not matched securities or data coverage. If the user asked only for a design, present the validated program as unexecuted.

## Execute and retrieve

When the user asks for matching stocks or a count, execute the screen; the request authorizes an execution receipt. Call `fintel.run_screen` with exactly one of `program` or an owned `screenId`. This creates a private, expiring receipt and does not create a saved screen. Use an optional `requestKey` for retries of the same intent; do not reuse it for a changed program or parameters.

Read `structuredContent.data` (also serialized in the MCP text content). Pass returned `run_id` as `runId` to `fintel.get_screen_run`. Poll `queued`/`running` until `succeeded`, `failed` or `cancelled`; pending is not an empty result. Jobs run through the existing queue drain, so do not claim completion from a submission receipt.

Only `succeeded` establishes matches. Follow `next_offset` as `offset` with the same `runId` until null when complete coverage is needed. The page `limit` is separate from the program's DSL `limit`. `total_rows` counts the program's output after its DSL limit; a top-25 result cannot establish an unrestricted population count. For a full count, execute a program without that DSL limit, subject to server bounds.

Report returned country/symbol/name identities, selected values, program, evaluation anchor and execution time, with units and coverage. `retrieved_at` is execution time; per-value observation/publication dates remain unknown. Missing comparisons are false and null is unavailable, never zero. Historical screening uses the current listing universe and does not guarantee historical constituents or publication-time availability. An unordered limit does not establish a ranked top-N.

Failed/cancelled runs publish no partial results. Inspect `error_code`: refine filters or add a disclosed DSL limit for `result_limit_exceeded`; explain provider/evaluation failures as unavailable evidence. Expired receipts need a new run/key. Use `fintel.cancel_screen_run` when the user asks to stop a pending run.

## Saved screens and history

For user-requested account work, use `fintel.list_screens` then `fintel.get_screen` to obtain owned IDs and inspect definitions. `fintel.create_screen`, `fintel.update_screen` and `fintel.delete_screen` persist changes visible in Workbench; explain the concrete change and require explicit user intent. A request to find stocks does not authorize saving, replacing or deleting a definition. Updates replace the definition; omitted summary clears it. Deletion also removes related stored results/history/backtests.

`fintel.get_screen_performance` reads stored scheduled history. `fintel.list_screen_backtests` and `fintel.get_screen_backtest` read existing saved web artifacts.

For a requested new historical replay, validate then call `fintel.run_screen_backtest` with program XOR screenId, `startDate`, `endDate`, `interval` (`day`, `week`, `month`) and optional `requestKey`. Poll/page using the same run tools. Follow live date/evaluation limits. This is trade-membership replay with mean closed-trade return, not portfolio total return. It omits portfolio weights, cash, slippage, costs, dividend reinvestment and benchmark total returns; open positions are unmarked. Disclose current-universe and publication-time limitations before interpreting performance.

Examples: “Find US small caps trading below net assets”; “How many companies match these criteria?”; “Save this validated screen”; “Backtest this screen monthly over the last year.”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.
