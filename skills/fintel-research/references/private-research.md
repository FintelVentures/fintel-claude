# Private saved research

These tools apply only to authorized private personal research. Do not call them for a public
company briefing or bring their output into a team/public response. Resolve a listing, then use
`fintel.get_research_context` for compact saved thesis summaries when personal continuity is
requested. `fintel.search_research` finds owned theses; `fintel.get_research_thesis` reads a selected
version, `fintel.list_research_versions` lists history and `fintel.compare_research_versions`
compares saved records. Saved beliefs and evidence receipts are not fresh verified financial data.

`fintel.check_thesis_evidence` reads one owned thesis/version against retained sources. Preserve
`baseline_verification`, original/current references, cutoff and coverage. SEC references compare
the same concept/unit/period; superseded means a newer filing for that same period. Scalar
references have a user-supplied unverified baseline; an exact date differs from latest mode, and
a new effective date can be changed even when the value is equal. Distinguish unchanged, changed,
superseded, now_unavailable and not_checkable. Unchanged does not establish freshness. Checks do
not download/index data, rewrite evidence, mark a review or start monitoring.

`fintel.create_research_thesis` and `fintel.revise_research_thesis` persist complete immutable
snapshots. Show the exact proposed snapshot and reason, obtain approval of that content, then
set `approved=true`. Preserve authorship separately; revisions use the previewed `expected_version`.
Use a fresh idempotency key for a new operation and identical arguments/key for an uncertain retry.
Copy supported source references unchanged from actual returned evidence, with exact values,
units and dates; a source reference is not proof of a calculated result. Never invent references.
`fintel.delete_research_thesis` permanently removes all versions/evidence: read the latest version
and obtain explicit approval of the named thesis and full deletion scope. None of these operations
enables alerts, background monitoring or publication.

Evaluation cases:
- Public/team research: no personal thesis reads or disclosure of personal holdings/beliefs.
- Saved thesis says unchanged: explain checked source coverage and unknown freshness.
- Revise request: preview complete replacement and reason; do not treat background review as approval.
- Uncertain write outcome: retry identical arguments/key rather than creating duplicate versions.
