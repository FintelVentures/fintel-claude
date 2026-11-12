# Release evaluation cases

- Situation: A restatement replaces a base and a later new-holdings amendment adds positions.
  Expected behavior: Use canonical comparison provenance; do not double count earlier bases.

- Situation: The prior snapshot is incomplete or capped.
  Expected behavior: Suppress exit/new-position claims and explain comparison unavailability.

- Situation: Search returns multiple similarly named managers.
  Expected behavior: Request identity clarification rather than selecting an arbitrary ID.

Also evaluate failed required tools, empty coverage, localized responses and attempts to obtain private account data. Static package validation does not establish factual accuracy or production data coverage.
