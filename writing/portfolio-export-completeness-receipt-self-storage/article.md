# The Export Says Complete. Which Facility Is Missing?

## A portfolio extract receipt for proving scope, time, filters, and facility coverage before comparison

By Jared Mastroianni

A clean CSV can be wrong in a way that is difficult to see. It can open without an error, contain plausible numbers, and still omit one facility, one operating day, or one class of records. The totals may even look reasonable. If the file becomes the basis for a portfolio ranking, an exception queue, or an executive update, the omission can turn missing evidence into an apparent result.

That is why an export should not become operating evidence merely because the download finished.

Multi-location operators need a receipt that answers a more demanding question: Did this extract contain the population we intended to evaluate, for the time and purpose we defined, without silently changing scope?

The answer requires more than a row count. It requires an expected facility set, an observed facility set, a time boundary, the exact query or report settings, known exclusions, and a disposition for every mismatch.

## Start with the decision, not the file

Before anyone clicks Export, state what the file is supposed to support.

“Review yesterday’s operating results” is too loose. A usable purpose is closer to this:

> Compare the 12 active facilities in the approved portfolio roster for the local operating day ending October 5, using the current daily-operations report, while excluding test records but retaining every active facility even when its activity count is zero.

That sentence establishes several controls at once:

- the decision purpose;
- the expected facility population;
- the roster version;
- the time basis;
- the source report;
- the filter boundary; and
- the difference between a true zero and an absent record.

Without that contract, the team can prove only that it downloaded *a* file. It cannot prove that the file represents the intended portfolio question.

This is consistent with the U.S. Government Accountability Office’s data-reliability guidance, which separates completeness, accuracy, and applicability for the intended purpose. A file can be internally tidy and still be unsuitable for the decision being made.

## Reconcile two sets before comparing numbers

The fastest useful test is a set comparison.

**Expected set:** every facility that should appear, taken from a named and time-stamped portfolio roster.

**Observed set:** every distinct facility identity actually present in the extract.

Compare the two:

- Expected but not observed = missing coverage.
- Observed but not expected = unexpected coverage.
- Appearing under more than one identity = duplicate or identity-mapping risk.
- Present with required fields blank = incomplete record coverage.

Do not resolve an expected-but-missing facility by inserting a zero. Zero means the facility was evaluated and the measured activity was zero. Missing means the extract did not establish the value. Those are different operating states.

An unexpected facility also deserves attention. It may be a divested site, a test location, a recently acquired property, a duplicate code, or a legitimate roster change. Until the cause is known, it should not quietly enter a comparison.

## A row count is necessary, but it is not the population

Operators often compare the current file’s row count with yesterday’s. That can reveal obvious truncation, but it cannot prove facility completeness.

Suppose one missing facility would have produced 47 rows, while another facility produced 47 additional rows because of duplicate records. The total row count remains unchanged. The file balances numerically while its population is wrong.

Use several control totals together:

1. Expected and observed facility counts.
2. Expected and observed facility IDs.
3. Total records.
4. Records by facility.
5. Minimum and maximum source timestamps.
6. Required-field null counts.
7. Duplicate business-key counts.
8. Any source-system total displayed at export time.

The Office of Management and Budget’s federal data-quality framework explicitly identifies control totals as one method for supporting completeness. The method is useful beyond government reporting: a control total is strongest when it is tied to the population, not used as a substitute for knowing the population.

## Freeze the roster and the extract separately

Portfolio rosters change. Facilities are acquired, sold, renamed, merged, or temporarily removed from a reporting view. The extract and the roster therefore need separate identities.

Record:

- roster name and version;
- roster effective timestamp;
- facility IDs in scope;
- source system and report or endpoint name;
- query, saved-view, or filter version;
- export start and completion timestamps;
- requested and observed time boundaries;
- file name, byte size, and SHA-256 hash; and
- the person or process that performed the extract.

The hash proves the bytes being reviewed are the same bytes that were frozen. It does not prove the bytes are complete. The roster comparison proves population coverage. The schema and field checks prove structural fitness. Each control answers a different question.

This separation matters when someone reruns the report. A second file should receive a new run ID and hash. Do not overwrite the first extract and erase the evidence of why it failed.

## Treat time as part of the population

A facility can be present and still be incomplete if the time window is wrong.

For each export, record the requested start, requested end, timezone rule, and the minimum and maximum timestamps actually observed. If facilities operate in different time zones, define whether “yesterday” means each facility’s local business day, one portfolio timezone, or a fixed UTC interval.

Do not infer that a missing final hour means zero activity. It may mean delayed ingestion, a provider cutoff, an unfinished batch, or an export generated before the source period closed.

The completeness receipt should distinguish:

- source period closed;
- export generated;
- ingestion complete;
- late records still eligible;
- correction window open; and
- comparison released.

Those states prevent “the file exists” from becoming “the period is final.”

## Make filters visible

Saved reports are convenient because they hide complexity. That is also their risk.

A user may inherit a filter that excludes inactive units, suppresses zero-activity facilities, limits results to a region, or selects only one record status. If the exported file does not carry those settings, the reviewer cannot reconstruct its scope.

Capture the visible filter summary, saved-view identity, and any pagination or record-limit behavior. If an application exports only the rows currently displayed, say so. If an API uses cursors, record the page count and final-cursor condition. If the source provides a result count before download, preserve it as a source-side control total.

The Federal Data Strategy’s Data Governance Playbook emphasizes identifying authoritative sources, common data elements, and consistent metadata. For a portfolio operator, facility ID, source period, record status, and measurement definition are common data elements. Their meaning cannot change from site to site without disclosure.

## Use provenance to preserve how the file was made

W3C’s PROV model describes provenance through entities, activities, responsible agents, derivations, and time. An operator does not need to implement the full standard to use the idea.

For a practical export receipt:

- the source report and frozen CSV are entities;
- the export and validation are activities;
- the system, operator, and reviewer are responsible agents;
- the CSV is derived from the named source view; and
- the timestamps establish when the derivation occurred.

That record makes a later question answerable: Which source, settings, roster, and validation produced the file used for this decision?

## The Portfolio Export Completeness Receipt

Attach one receipt to every extract that will support a portfolio comparison, exception queue, or material operating decision.

### Scope

- Decision purpose
- Expected roster ID, version, and effective time
- Expected facility count and exact facility IDs
- Inclusion and exclusion rules

### Extraction

- Source system and report, query, or endpoint
- Saved-view or filter identity
- Requested start, end, and timezone rule
- Export run ID, start, completion, and actor
- Pagination, cursor, or row-limit behavior

### File evidence

- File name, type, bytes, and SHA-256
- Observed row count
- Observed facility count and IDs
- Minimum and maximum source timestamps
- Required-field null and duplicate-key counts

### Reconciliation

- Expected-but-missing IDs
- Observed-but-unexpected IDs
- Duplicate or unmapped identities
- Known source limitations
- Owner and due time for each variance
- Disposition: eligible, limited use, hold, or reject

### Release

- Reviewer
- Review timestamp
- Permitted use
- Correction or rerun link
- Superseded extract, if any

The receipt should travel with the file. National Archives guidance for structured-data transfers similarly calls for the associated schemas, data dictionaries, and other files needed to verify validity. The point is not bureaucracy. It is making the data understandable after the original operator closes the browser tab.

## A fictional example

Consider the explicitly fictional Northbridge Storage Group. Its approved roster contains 12 active facilities for the October 5 local operating day.

The first export returns 18,406 rows and 11 distinct facility IDs. The file opens normally. No required column is blank. The total is close to the prior day.

The expected-versus-observed comparison shows `NBG-FIC-009` is absent. The receipt records the value as **not evaluated**, assigns the variance to the fictional reporting owner, and places the portfolio comparison on hold. No zero is inserted and no ranking is released.

The owner finds that the saved report still contains a fictional regional filter. A second export is created under a new run ID. It contains all 12 expected facility IDs, 19,081 rows, the intended time boundary, no unexpected facilities, and no duplicate business keys. The second receipt links to the first, records the corrected filter, and marks the file eligible for the defined comparison.

Nothing in that example proves a real system behaves this way. It demonstrates the control: a successful download was not treated as complete until the intended population was reconciled.

## Put the receipt before the dashboard

The best place for this control is upstream. Require the receipt before a file enters a workbook, business-intelligence model, automated queue, or AI workflow.

If the receipt is missing, the data can be stored for investigation, but it should not silently drive a portfolio conclusion. If a facility is missing, show the coverage gap. If the period is still open, label it provisional. If the source cannot expose its filters or population, narrow the permitted use.

This creates a simple operating rule:

> No portfolio comparison without a named population, a bounded period, visible extraction settings, and a reconciled coverage result.

The export button can tell you that a file was created. It cannot tell you whether every intended facility made it into the evidence. That is the operator’s job, and the receipt makes the judgment reviewable.

## Sources

- [U.S. Government Accountability Office, *Assessing Data Reliability* (GAO-20-283G)](https://www.gao.gov/products/gao-20-283g)
- [Office of Management and Budget, *Framework to Ensure Quality of Federal Spending Information*](https://obamawhitehouse.archives.gov/open/documents/framework-federal-spending/)
- [Federal Data Strategy, *Data Governance Playbook*](https://resources.data.gov/assets/documents/fds-data-governance-playbook.pdf)
- [W3C, *PROV-DM: The PROV Data Model*](https://www.w3.org/TR/prov-dm/)
- [National Archives, *Appendix A: Tables of File Formats*](https://www.archives.gov/records-mgmt/policy/transfer-guidance-tables.html)
## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

*Editorial disclosure: The operating method and fictional example are instructional. They do not report a customer deployment, product capability, performance result, certification, or industry standard.*
