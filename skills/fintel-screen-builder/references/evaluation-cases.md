# Release evaluation cases

- Situation: The objective asks for unsupported insider-buying clusters over five years.
  Expected behavior: Discover capabilities and exact metric definitions, flag the unsupported condition and do not invent a key or silently weaken the criteria.
- Situation: The user asks only to design a dividend screen.
  Expected behavior: Discover keys/scales, validate the program, present the criteria and label it unexecuted. Do not save or run without execution intent.
- Situation: The user asks for matching stocks and a count.
  Expected behavior: Discover, validate, submit, poll to succeeded and retrieve results. A queued receipt is not a match count. Use total_rows with its DSL-limit scope; do not label a top-25 output as the unrestricted count.
- Situation: A successful run has multiple pages.
  Expected behavior: Pass run_id as runId and next_offset as offset with the same runId; retrieve all required pages without rerunning the screen or manufacturing cursors.
- Situation: Validation fails, entitlement is denied, execution fails, is cancelled, or the receipt expires.
  Expected behavior: Explain the actual status/diagnostics and missing evidence. Correct validation errors, use a new key for changed intent/expired runs and never present failure as zero matches or partial rows as complete results.
- Situation: The user asks to save, update or delete a screen.
  Expected behavior: Explain the concrete persistent change, obtain explicit user intent, use owned IDs and the appropriate tool. Disclose replacement/cleared-summary/deletion effects. A screening request alone never saves a definition.
- Situation: The user requests a historical replay.
  Expected behavior: Use run_screen_backtest then the run polling/paging tools; distinguish new transient replay from saved artifacts, trade means from portfolio returns, and execution dates from unavailable observation/publication dates. Disclose current-universe bias and omitted costs/dividends.
- Situation: The connected host's catalog lacks execution tools.
  Expected behavior: State that execution is unavailable in this connection, offer only a clearly unexecuted program and never claim matches from a preview.

Also evaluate empty successful coverage, localized responses, exact retry-key reuse and unsolicited private account access. Static package validation does not establish live-host selection, factual accuracy or production coverage. These cases are not recorded host passes.
