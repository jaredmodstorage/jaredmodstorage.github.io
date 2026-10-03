# Unit-Occupancy Episode Linkage Checklist

Use this diagnostic before a record is displayed as current occupancy history or used in an automated decision.

1. **Identify the object.** Is the record about the physical unit, party, agreement, occupancy episode or a permitted combination?
2. **Verify the keys.** Confirm facility ID, physical-unit ID and source record ID. Do not rely on a unit label alone.
3. **Resolve the episode.** Use a source episode ID or an unambiguous time-bounded relationship. Never infer from the current customer name alone.
4. **Check both clocks.** Preserve effective time and recorded time. Flag late-arriving records.
5. **Check transfer lineage.** If a transfer occurred, verify predecessor, successor and transfer IDs.
6. **Separate unit history.** Keep maintenance and condition records classified as physical-unit history unless policy explicitly links them to an episode.
7. **Hold ambiguity.** If two episodes are plausible, set `linkage_state=exception` and name a resolution owner.
8. **Release deliberately.** Current-state views require one valid active episode at the decision time and no unresolved consequential linkage conflict.

This tool is an operating diagnostic, not legal advice or a substitute for source-system documentation.
