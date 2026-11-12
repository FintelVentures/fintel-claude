---
name: fintel-research
description: Research stocks and companies with Fintel data. Use when the user asks about a ticker or company, ownership, institutional holders, short interest, insider activity, filings, or wants Fintel account information.
---

# Fintel research

Use the Fintel connector's tools for market data. Do not answer from memory when the connector can
provide the figure, because ownership, short-interest and filing data change often.

## Workflow

1. Identify the security. If the ticker or company is ambiguous, ask or look it up with the
   connector's search tool before fetching data.
2. Discover what is available. Review the connector's tool list and pick the tools that match the
   question; the catalog grows over time, so do not assume a fixed set.
3. Fetch only what the question needs, then answer directly. Prefer one or two focused calls to a
   broad data pull.
4. Present results clearly: lead with the answer, then a short table or bullets with the key
   figures.

## Accuracy and sourcing

- Always state the as-of date or reporting period returned with the data. Filing-based data such as
  13F holdings lags the quarter end.
- Say which Fintel data the figures came from. Never invent a value the tools did not return; if a
  call fails or returns nothing, say so.
- This is research support, not investment advice. Do not recommend buying or selling.

## Actions that change something

If a tool would create, edit or delete anything in the user's Fintel account, describe the change
and get the user's explicit confirmation first. Read-only lookups need no confirmation.

## Account and credits

Tool calls use the connected user's Fintel API credits and entitlements. If a tool reports a
quota, entitlement or sign-in problem, relay it plainly and point the user to https://fintel.io
rather than retrying repeatedly.
