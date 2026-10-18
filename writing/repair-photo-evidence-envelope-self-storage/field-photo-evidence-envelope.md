# Field Photo Evidence Envelope

Use this tool for photographs that may influence a work-order, inspection, incident, invoice, warranty, acceptance, or release decision across a self-storage portfolio. It is an operating-record design aid, not a digital-forensics procedure, legal hold, privacy policy, evidence-admissibility opinion, or substitute for qualified inspection.

## 1. Identity binding

- Assign one evidence ID.
- Record stable facility ID and current human-readable name.
- Record asset ID or bounded area description; do not invent an asset ID.
- Record local label as a separate field.

**Pass:** a reviewer can distinguish this facility and object from similar sites and assets.

## 2. Event binding

- Link the work visit, work order, incident, inspection, or acceptance review that caused the photo.
- Record authorized scope separately from work reported as performed.
- Do not use a prior visit’s image to close a later event.

**Pass:** the image belongs to one identified operating episode.

## 3. Capture and receipt

- Record photographer identity or role under policy.
- Preserve device-reported capture time and time-zone context when available.
- Preserve system receipt time separately.
- Record source device or capture channel without storing unnecessary personal data.

**Pass:** capture and system-receipt facts are explicit and conflicts are visible.

## 4. Original-file integrity

- Retain the original file when policy permits.
- Record original filename, media type, byte count, SHA-256 hash, and controlled storage reference.
- Record content-credential state and location-data state as present, absent, unavailable, or not collected.
- Never treat a matching hash or credential as proof that the caption is true.

**Pass:** the original can be distinguished from copies and derivatives.

## 5. Observation and claim boundary

- Describe only what is visibly present.
- Store the uploader’s caption separately.
- Store the proposed operational claim separately.
- Identify overview, detail, identification, before, during, or after view.

**Pass:** observation, report, claim, decision, and readback are not collapsed.

## 6. Derivative and correction lineage

- For crop, annotation, compression, conversion, or redaction, create a derivative ID and parent link.
- Record the operation and responsible role.
- If attached to the wrong record, invalidate the link with reason and correction history; do not erase the original event.

**Pass:** every derivative and corrected attachment traces to its parent and decision history.

## 7. Privacy, access, and retention

- Review for people, customer property, plates, credentials, account data, and other restricted content.
- Apply approved access roles and redaction state.
- Apply the approved retention class and disposition date.
- Do not copy governed imagery into personal camera rolls, text threads, or uncontrolled folders.

**Pass:** legitimate operational use is bounded by need-to-know access and retention controls.

## 8. Decision and readback

- Record the completion claim and authorized decision owner.
- Identify required views and whether the set is complete.
- Record qualified inspection or test when policy requires it.
- Record independent operating readback separately from the photo.
- Assign every exception an owner and due time.

**Pass:** the decision relies on the full required record, not the image alone.

## Quarantine codes

- `IDENTITY_CONFLICT`
- `EVENT_LINK_MISSING`
- `DUPLICATE_HASH_CONFLICT`
- `ORIGINAL_UNAVAILABLE`
- `TIME_CONFLICT`
- `PRIVACY_REVIEW_REQUIRED`
- `DERIVATIVE_PARENT_MISSING`
- `CAPTION_OVERCLAIMS_FRAME`
- `REQUIRED_VIEW_MISSING`
- `READBACK_PENDING`

Promote the image only after the conflict is resolved, the claim is narrowed, the record is replaced, or the evidence is explicitly marked unusable for the proposed decision.
