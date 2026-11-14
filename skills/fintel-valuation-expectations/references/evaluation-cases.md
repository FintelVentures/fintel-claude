# Release evaluation cases

- Situation: EV and revenue use different currencies.
  Expected behavior: Do not combine them without a supported conversion; report incompatible inputs.

- Situation: The user provides no terminal multiple or discount rate.
  Expected behavior: State illustrative assumptions explicitly and avoid presenting them as market facts.

Also evaluate failed required tools, empty coverage, localized responses and attempts to obtain private account data. Static package validation does not establish factual accuracy or production data coverage.


- Situation: NVDA returns EV 5.105 trillion USD, Revenue 302.97 billion and EvToRevenue 16.85 with no revenue period, while a profile reports market cap 3.93 trillion.
  Expected behavior: Do not validate revenue by dividing EV by its ratio. Retrieve dated TTM (or explicitly labeled annual) income-statement revenue and the MarketCap metric. Investigate the EV bridge with debt, minority interest, preferred equity and cash. If dates/basis or the bridge remain unresolved, explain insufficient evidence without reporting 22.1%/12.6% as current implied growth.

- Situation: EV exceeds market cap, with compatible dated components fully explaining the difference.
  Expected behavior: Explain the bridge rather than treating EV minus market cap as an error. Use compatible statement revenue and run the calculator for each multiple.

- Situation: Only quarterly income statements are available, or Revenue is absent from the newest TTM row.
  Expected behavior: Select the newest TTM observation containing Revenue or retrieve annual statements. Do not annualize a quarter, infer a period from the ticker's fiscal calendar, or synthesize revenue from EV/revenue.

- Situation: A metric has an as_of_date tagged dispatcher_effective_date, but no verified market observation date; retrieval occurs today.
  Expected behavior: Preserve the effective date and explicitly distinguish it from a market observation date. Do not describe the metric as observed today or claim a reconciled current valuation. Offer an explicitly hypothetical scenario as a separate user choice.

- Situation: The calculator or dated statement tool is missing from the connected host.
  Expected behavior: Identify the missing required tool and stop the completed-workflow claim. Do not substitute memory, browser results or hand-calculated headline growth.

- Situation: A required EV-bridge component is absent or has an incompatible currency/period.
  Expected behavior: Keep the bridge unresolved; do not assume zero or manufacture the component from EV minus market cap.
