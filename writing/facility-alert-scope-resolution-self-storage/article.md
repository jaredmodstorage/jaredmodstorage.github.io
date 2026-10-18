# The Alert Names a County. Which Facilities Are Actually in Scope?

## A multi-location operator needs a governed location record, the full alert geography, and a facility-by-facility resolution before assigning work

By Jared Mastroianni

<!-- BODY START -->

A regional operator receives an official alert naming a county. Three facilities have mailing addresses in that county. One sits inside the alert polygon. One is outside the polygon but inside the same county. The third is near a forecast-zone boundary that does not match the county line.

The fastest response is to send the same instruction to all three sites. It is also the easiest way to confuse receipt with scope.

An alert is authoritative about its own content. It does not know a company’s facility master, operating modes, staffing plan, customer commitments, or local release authority. The portfolio’s job is to preserve the source alert, resolve its geography against governed facility locations, assign the right action to each facility, and keep uncertainty visible.

That requires more than searching an address or matching a ZIP code. It requires a repeatable alert-scope resolution system.

## Start with the alert as a versioned record

The first control is simple: keep the alert intact before translating it into tasks.

The National Weather Service distributes watches, warnings, advisories, and similar products through its alerts service using the Common Alerting Protocol, or CAP. CAP gives an alert a structured identity and lifecycle. The record can include an identifier, sender, sent time, status, message type, scope, event, urgency, severity, certainty, effective and expiration times, instructions, references, and an area represented through descriptions, geographic codes, polygons, or circles.

Those fields should not be flattened into a notification such as “storm alert — call the stores.” Preserve the source identifier and retrieval time. Preserve whether the message is an actual alert, an update, or a cancellation. Preserve the referenced prior message when one exists. Preserve the original geography even if the portfolio later creates a simplified operating view.

The operational reason is revision control. A manager who acts on the first message while the portfolio dashboard shows an updated boundary must be tied back to the exact alert version received. Otherwise, a later review cannot distinguish a late acknowledgment from a changed scope.

The source record is not a screenshot. A screenshot can help a person understand what was visible, but it is weak as the only machine-readable evidence of identifier, lifecycle, timestamps, references, and geographic fields.

## A county, a forecast zone, and a polygon are not interchangeable

The National Weather Service’s geolocation guide draws an important distinction between county Universal Geographic Codes and NWS-managed public forecast or fire-weather zones. Those zones do not have a one-to-one relationship with physical counties. They can cross county lines or cover only part of a county.

Some rapid-onset warnings include polygon geometry. Other county-based alerts may have no polygon and instead identify the area through county codes. Longer-duration products may use public forecast or fire-weather zones, also without alert geometry. The same provider therefore may describe “where” in different ways depending on the product.

This matters when a portfolio builds queries. The NWS guide warns that querying only by a forecast-zone identifier can omit county-based alerts. A point query resolves both the county and zone codes intersecting that coordinate. That does not make one point query a complete emergency system, but it shows why a single zone list is a fragile substitute for facility-level resolution.

The portfolio resolver should accept multiple geographic forms:

- polygon or circle geometry when the source provides it;
- county codes when the product is county-based;
- public forecast or fire-weather zone codes when the product is zone-based;
- the provider’s human-readable area description; and
- an explicit unresolved state when the available data cannot support a reliable match.

Do not force every alert into the same boundary type. Normalize the structure without pretending the underlying geographies are equivalent.

## Govern the facility point before the alert arrives

An alert resolver is only as trustworthy as the facility location record it receives.

Each operating facility should have a stable facility ID and a governed location profile. At minimum, that profile should carry the approved street-address record, a coordinate pair, the source and date of that coordinate, the county code, relevant NWS public and fire-weather zones, the location-record version, and the owner responsible for correcting it.

A mailing city, postal code, marketing label, or regional nickname is not enough. A ZIP code is a delivery construct, not proof that a facility sits inside a particular alert polygon or forecast zone. A facility name can also outlive a management change, street renumbering, parcel combination, or data migration.

Location changes deserve the same release discipline as other master data. When the coordinate, address, county, or zone relationship changes, record the effective version, test downstream consumers, and reconcile the systems that cache the old value. The weather feed should not quietly repair facility master data during an event.

If a facility’s governed coordinate is missing, stale, or disputed, classify the match as unresolved. Route that record to a named human owner. “Probably the right location” is not a safe portfolio state.

## Resolve scope facility by facility

The resolver should produce a decision table, not a portfolio-wide yes-or-no flag. A practical match vocabulary is:

1. **Included by source geometry.** The governed facility point falls inside a source polygon or circle.
2. **Included by county code.** The source defines the affected area at the county level and the governed facility county matches.
3. **Included by NWS zone.** The source uses a public or fire-weather zone and the facility’s governed zone matches.
4. **Outside the represented area.** The governed point and codes do not match the source geography used for that alert.
5. **Adjacent or monitoring.** The facility is outside the represented area, but an approved operating rule calls for monitoring because of proximity, shared infrastructure, a travel route, or another named dependency.
6. **Unresolved.** Source geography or facility location evidence is missing, conflicting, stale, or technically unreadable.

The match record should say which method produced the state and which evidence supports it. An included-by-county result is not the same as an included-by-polygon result. Neither is automatically proof of a condition at the property.

FEMA’s IPAWS material describes local targeting as a way for public alerting authorities to direct information to affected geographic areas. It also makes clear that alert content and timing remain with the alerting authority. For a self-storage operator, that means the official message remains the source for the public alert; the portfolio layer should not rewrite the hazard or claim to narrow the authority’s intended audience.

## Turn scope into bounded work, not automatic conclusions

Once a facility is matched, the system can select a prepared operating template. That template might ask the site to review the official alert, confirm staff receipt, apply the facility emergency or severe-weather plan, inspect an approved pre-event checklist from a safe position, protect a specific route, or report a local condition.

The template must still preserve decision authority. A geographic match does not prove damage, unsafe access, a power failure, customer impact, or the need to close. An outside result does not override local emergency direction, an observed site condition, or a provider update. An unresolved result should not disappear from the queue merely because the rest of the portfolio resolved cleanly.

Keep these states separate:

- **source alert active** — the provider record is current under its own lifecycle;
- **facility in scope** — the portfolio resolved the facility against that alert geography;
- **work assigned** — an approved task was issued to an accountable role;
- **receipt acknowledged** — the facility or regional owner confirmed receipt;
- **action completed** — the assigned step was reported complete;
- **evidence verified** — the required readback supports the claimed step; and
- **operating state released** — the authorized owner changed the facility’s operating status.

A push notification proves none of the later states. A completed checklist does not cancel the alert. An alert cancellation does not prove that local consequences have been assessed or that a restricted area is ready to reopen.

## Follow the message chain through updates and cancellations

Alerting systems are not static. CAP distinguishes message types and provides references that can connect a new message to earlier records. The NWS alerts documentation also describes the use of references across message series.

The portfolio should therefore maintain one alert family with multiple source versions. When an update arrives, recompute scope against the new geography and show the delta: facility added, facility removed, still included, still outside, or unresolved. Do not overwrite the original match. When a cancellation or expiration arrives, close the source-alert state while preserving any local tasks that require separate review.

This is where many dashboards become misleading. They display the newest banner but discard the operating trail. A regional leader then sees “cancelled” without knowing that one site still has a blocked drive aisle, an unacknowledged staff message, or a pending public-authority instruction.

## The operator tool: Facility Alert-Scope Resolution Grid

The companion grid joins four records without collapsing them: the source alert and its version; the governed facility location; the match method and scope state; and the facility work, acknowledgment, evidence, and release trail.

The blank template is suitable for implementation planning. The Cedar Span Portfolio rows are explicitly fictional teaching records. They do not represent a real alert, facility, location, county, zone, customer, employee, emergency, deployment, provider result, response time, damage, closure, or reopening.

## Fictional example: four facilities, four honest states

In the fictional Cedar Span Portfolio, an invented alert record includes a polygon, county codes, and an expiration time. The portfolio has four fictional facilities.

Cedar Span North resolves inside the fictional polygon and receives the approved local-plan review task. Cedar Span South shares a county label but its governed point is outside the polygon; the record stays outside the represented geometry rather than inheriting North’s result. Cedar Span Ridge matches a fictional zone-based companion record and is classified by zone, not by county. Cedar Span Harbor has a disputed coordinate after an address correction, so the resolver refuses to decide and assigns a human location-data review.

An invented update changes the polygon. The system stores a new match version, adds South to the represented area, preserves North’s prior decision trail, and leaves Harbor unresolved. A later fictional cancellation closes the source-alert state. It does not close a separate local access restriction reported at Ridge; the authorized operating owner reviews that condition on its own evidence.

The lesson is not that a portfolio should automate emergency judgment. It is that geography, source lifecycle, facility identity, assigned work, and operating release should remain traceable when the situation is moving quickly.

## Make the portfolio answer one question clearly

At any moment, an operator should be able to ask: “Why is this facility in—or out of—this alert workflow?”

The answer should fit in one record: exact alert version, exact facility location version, match method, evidence, current scope state, assigned action, acknowledgment, unresolved issue, next review, and release owner.

That is the difference between broadcasting an alert and operating a portfolio. The first moves a message. The second preserves enough meaning for each facility to receive the right work—and for the organization to explain the decision later.

<!-- BODY END -->

## Sources

1. National Weather Service, [Alerts Web Service](https://www.weather.gov/documentation/services-web-alerts). Accessed October 11, 2026.
2. National Weather Service, [NWS Watch, Warning, and Advisory Alerts Geolocation Guide](https://www.weather.gov/media/documentation/docs/NWS_Geolocation.pdf). Accessed October 11, 2026.
3. OASIS, [Common Alerting Protocol Version 1.2](https://docs.oasis-open.org/emergency/cap/v1.2/CAP-v1.2-os.html). OASIS Standard, July 1, 2010; accessed October 11, 2026.
4. Federal Emergency Management Agency, [IPAWS 101](https://www.fema.gov/sites/default/files/documents/fema_ipaws_101-slicksheet_042024.pdf). January 2024; accessed October 11, 2026.

## Author

Jared Mastroianni is Chief Operating Officer of modSTORAGE and CEO and Founder of Facily.ai.

## Editorial disclosure

Cedar Span Portfolio and every associated alert, identifier, message, polygon, county, zone, facility, address, coordinate, customer, employee, authority, provider, work item, observation, decision, response, restriction, closure, release, time, and outcome are fictional. The governed image is an AI-generated editorial illustration, not documentary evidence of an alert, facility, event, meeting, customer, employee, authority, deployment, or result. This article and tool were produced with AI assistance under human direction and review. The method is an operating-design proposal, not emergency-management, public-warning, meteorological, GIS, legal, regulatory, engineering, safety, or site-specific compliance advice. Official alerts, public authorities, facility emergency plans, employer policies, and qualified local decisions govern actual events.
