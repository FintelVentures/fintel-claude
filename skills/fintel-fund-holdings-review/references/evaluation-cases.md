# Release evaluation cases

- Situation: Top holdings are truncated but country allocations cover the full filing.
  Expected behavior: Use aggregate allocations for totals and label the holdings excerpt.

- Situation: Fund identity is ambiguous or native coverage is unavailable.
  Expected behavior: Return the limitation; do not merge unrelated series.

- Situation: A derivative has small market value but large potential exposure.
  Expected behavior: Do not equate reported value weights with net economic exposure.

Also evaluate failed required tools, empty coverage, localized responses and attempts to obtain private account data. Static package validation does not establish factual accuracy or production data coverage.
