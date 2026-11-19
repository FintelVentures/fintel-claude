---
name: fintel-screen-builder
description: Design, validate and execute custom stock screens with Fintel Workbench. Use for compound filters, formulas, rankings, historical screening, backtests and user-requested saved screens; use stock-discovery for existing leaderboard shortlists.
---

# Screen builder

Use Fintel's authenticated MCP connector and inspect the live tool catalog and entitlement results. Start with `fintel.get_screening_capabilities` for the implemented language, function signatures, examples, workflow, limits and warnings. Universe screening does not require resolving an individual listing. If execution tools are absent from the connected host, explain the missing capability and label any proposed program as unexecuted; never invent matches.

Required evidence failures must remain explicit coverage gaps. Preserve returned units, currencies, missing values, dates and warnings. Cite material observations, distinguish facts from interpretation and assumptions, and write in the user's language. Do not replace missing Fintel observations with model memory.

Contract: `screen_builder` / `screen-builder-v3` (portable MCP workflow; does not change any separate server-side agent contract).

## Design and validation

1. Call `fintel.list_data_definitions`, respecting dictionary pagination, then `fintel.get_data_definition` for relevant returned keys. Never guess metric aliases or substitute unsupported historical or clustering conditions. A leaderboard shortlist is a different workflow.
2. Translate the objective into a complete semicolon-terminated Workbench program. Explain the universe, criteria, sorting, exclusions and missing-data policy. For each criterion preserve its exact key, operator, threshold and units; distinguish user-supplied thresholds from proposed assumptions. Ask a bounded clarification when an unresolved choice materially changes the criteria.
3. Follow the live capabilities for syntax and supported functions. Numeric scales vary by metric: the literal `5%` evaluates to `5`, not `0.05`. Named subqueries and dated aggregate sets are unsupported. Do not invent features.
4. Call `fintel.validate_screen` with `program`. Correct line/column diagnostics until `data.valid=true`; a validation success establishes syntax/access, not matched securities or data coverage. If the user asked only for a design, present the validated program as unexecuted.

## Execute and retrieve

When the user asks for matching stocks or a count, execute the screen. Call `fintel.run_screen` with exactly one of `program` or an owned `screenId`, plus optional `asOfDate`. The screen runs immediately in the serving JVM. This is one live call with no stored receipt, job queue or polling; do not supply a `requestKey` or call `get_screen_run` for a live screen. It does not create a saved screen.

Read `structuredContent.data` (also serialized in the MCP text content). The final successful result contains all rows and `total_rows`, with `partial=false`. Streamable HTTP hosts may request `params._meta.progressToken` and receive partial batch notifications in `params._meta["io.fintel/screening"]`; host support determines whether those updates reach the AI. Do not promise universal early result visibility. A preview is incomplete until the final call succeeds. The final rows replace any accumulated preview; do not append them twice.

`total_rows` counts output after the program's DSL `limit`; a top-25 result cannot establish an unrestricted population count. For a full count, execute a program without that DSL limit, subject to server bounds.

Report returned country/symbol/name identities, selected values, program, evaluation anchor and execution time, with units and coverage. `retrieved_at` is execution time; per-value observation/publication dates remain unknown. Missing comparisons are false and null is unavailable, never zero. Historical screening uses the current listing universe and does not guarantee historical constituents or publication-time availability. An unordered limit does not establish a ranked top-N.

A failed, cancelled or disconnected call invalidates earlier partial rows as a completed answer. Inspect returned execution errors: refine filters or add a disclosed DSL limit for `result_limit_exceeded`; explain provider/evaluation failures as unavailable evidence. The host can close the active stream to stop a live screen. There is no reconnect/resume receipt; a fresh call starts a new evaluation.

## Saved screens and history

For user-requested account work, use `fintel.list_screens` then `fintel.get_screen` to obtain owned IDs and inspect definitions. `fintel.create_screen`, `fintel.update_screen` and `fintel.delete_screen` persist changes visible in Workbench; explain the concrete change and require explicit user intent. A request to find stocks does not authorize saving, replacing or deleting a definition. Updates replace the definition; omitted summary clears it. Deletion also removes related stored results/history/backtests.

`fintel.get_screen_performance` reads stored scheduled history. `fintel.list_screen_backtests` and `fintel.get_screen_backtest` read existing saved web artifacts.

For a requested new historical replay, validate then call `fintel.run_screen_backtest` with program XOR screenId, `startDate`, `endDate`, `interval` (`day`, `week`, `month`) and optional `requestKey`. Poll/page with `fintel.get_screen_run`; use returned `run_id` as `runId` and `next_offset` as `offset`. Follow live date/evaluation limits. This is trade-membership replay with mean closed-trade return, not portfolio total return. It omits portfolio weights, cash, slippage, costs, dividend reinvestment and benchmark total returns; open positions are unmarked. Disclose current-universe and publication-time limitations before interpreting performance.

Examples: “Find US small caps trading below net assets”; “How many companies match these criteria?”; “Save this validated screen”; “Backtest this screen monthly over the last year.”

Read [evaluation cases](references/evaluation-cases.md) when validating this skill or preparing a release.

Preserve validation currency/unit diagnostics, not just syntax success. Do not combine incompatible
monetary metrics or interpret fraction/whole-percent units from a name alone. Historical FX must
use the returned dated evidence, not today's rate. For backtest receipts, read `run_id` as `runId`
and page with returned `next_offset` as `offset` through terminal status and all result pages.
`fintel.cancel_screen_run` is destructive for a historical receipt: it discards partial results
and cannot resume the run. Explain that effect and require an explicit cancellation request;
closing a live screen stream is a separate action.
