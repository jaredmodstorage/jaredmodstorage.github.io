# AI Observation-Gap and Imputation Integrity Gate

Use one record for each material gap and decision use. Do not edit the raw observation series to make it appear complete.

## 1. Identify the expected observation

- Resolve the exact facility, asset, measurement type, unit, source and expected cadence.
- Record the interval, expected sample count, observed count, missing count and coverage.
- Classify the cause as known, suspected or unknown. Do not infer normal facility conditions from a quiet source.

## 2. Preserve raw evidence

- Retain source record IDs, versions or hashes for every available observation.
- Preserve the missing interval as missing.
- Record quality states, rejected readings and source availability separately.

## 3. Govern any generated values

- Name the method, version, owner, parameters, assumptions and input references.
- Store generated values in a separate series or version.
- Assign an explicit value class such as `imputed`, `interpolated`, `derived` or `forecast`.
- Preserve an uncertainty representation and the original raw series.

## 4. Bind eligibility to one use

- Declare the intended use and consequence class.
- Apply deterministic rules for maximum gap, minimum coverage, permitted methods, corroboration and review.
- Record allowed and prohibited uses.
- Do not let a model confidence score override an ineligible evidence class.

## 5. Propagate the label

- Confirm that dashboards, exports, APIs, retrieval packets, prompts, summaries and decisions retain the value class and method reference.
- Reject a downstream artifact that presents a generated value as observed.
- Hand back unresolved high-consequence uses to a named owner with required evidence and a deadline.

## 6. Correct without rewriting history

- When a delayed observation arrives, preserve both the earlier estimate and the later observation.
- Create a correction record and compare the values.
- Identify affected summaries, alerts, decisions and actions.
- Route material corrections and verify governing-source readback before closure.

## Minimum release tests

Test complete data, isolated gaps, consecutive gaps, gaps beyond policy, delayed observations, source conflicts, unit conflicts, connector field loss, exports that omit flags and a model prompt that asks to fill blanks. A passing visualization alone does not establish safe downstream use.

The blank CSV is an implementation template. The Stonegate Hollow CSV is explicitly fictional teaching data and does not represent a real facility, sensor, system, policy, model, incident or outcome.
