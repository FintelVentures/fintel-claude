# Release evaluation cases

- Situation: Wide target spread with few analysts.
  Expected behavior: Explain dispersion and limited coverage without implying reliable probabilities.

- Situation: Rating counts change but no same-period estimate history exists.
  Expected behavior: Do not claim earnings-estimate revisions.

- Situation: Forecast periods are dated but consensus snapshot dates are missing.
  Expected behavior: Disclose unknown freshness rather than calling estimates current.

Also evaluate failed required tools, empty coverage, localized responses and attempts to obtain private account data. Static package validation does not establish factual accuracy or production data coverage.

- Situation: US EPS revision signals show a positive 30-day change but a missing 90-day baseline.
  Expected behavior: Report the 30-day fiscal target and receipt endpoints; retain the unavailable 90-day window and do not infer continuous upgrades.
- Situation: Current issuer-period reconciliation differs from retained provider-date history.
  Expected behavior: Preserve both identities; do not silently relabel historical targets or infer missing fiscal ends.
- Situation: Revision rankings exclude unknown currency/basis and nonpositive baselines.
  Expected behavior: Disclose excluded coverage; never turn missing comparisons into zero changes.
