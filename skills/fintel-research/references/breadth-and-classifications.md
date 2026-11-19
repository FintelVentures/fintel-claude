# Market breadth and classifications

Discover supported countries with `fintel.list_market_breadth`, then call
`fintel.get_market_breadth` with a returned country. Default reads return the latest accepted
observation. Use inclusive `start_date`/`end_date` and returned `meta.next_args` for bounded history.
For an exact date set both bounds; end-only reads may return an earlier accepted date.

Report the observation date, advance/decline/unchanged/comparable counts, resolved members,
coverage and latest-attempt status. Advance percent uses comparable members, not every resolved
member or the whole country's stock market. An insufficient latest attempt can coexist with an
older accepted observation. Empty history is missing coverage, never zero breadth.

When `analytics` is present, preserve each metric's status and denominator. Moving-average
percentages use eligible members for each 20/50/200-session measure. High/low counts use retained
52-week raw OHLC evidence, with history and corporate-action limits. Volume is shares, not dollars;
partial sums omit missing observations, and zero differs from null. Older observations may have
`analytics=null`; do not manufacture technicals. Raw prices and incomplete exchange calendars
limit interpretation. Keep calculation/revision provenance and warnings with historical results.

Exchange and Fintel GICS-equivalent sector groups partition the canonical country universe;
classification coverage differs from price coverage. Preserve UNKNOWN groups. Sector labels use
supported standard codes, but assignments use the current retained master rather than historical
point-in-time sectors. Index breakdowns are explicitly country subsets of stored public baskets,
not guaranteed complete official indices; configured and comparable member counts differ.

For taxonomy browsing start with `fintel.list_sectors` or `fintel.search_classifications`.
Use returned level/slug/path with `fintel.get_classification`,
`fintel.list_classification_children` and `fintel.list_classification_securities`.
`fintel.get_security_classification` reads a resolved listing's assignment. Discover supported
arguments from the live schema. Canonical sectors are separate from imported/unmapped roots in
`meta.other_categories`. `child_count` counts active immediate taxonomy children, not companies
or securities. Preserve assignment review flags: canonical taxonomy identity does not certify
company assignments. Use full returned paths for ambiguous slugs; never guess vendor codes.

Evaluation cases:
- 60% advancing among 10 comparable of 12 resolved members: show 83.333% coverage, not whole-market breadth.
- Accepted data predates an insufficient latest attempt: cite the accepted date and newer failure separately.
- Missing analytics or zero volume: preserve unavailable versus reported zero.
- Sector children and imported roots: do not turn child_count into a company count or imported roots into canonical sectors.
