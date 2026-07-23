# CTN — Open Questions

*The living open-questions deliverable required by Janus-Facing Architecture (standard check 7). Reviewed and re-shipped with each release; staleness is nonconformance. An entry leaves this document only by resolution or by an explicit values call made by the people who live with the outcome. A question that binds architecturally is promoted to the architecture document's Part VII, not kept local. Invariant IDs cite the registry in `JFA/jfa-conformance-suite.py`.*

CTN is the architecture's **high-stakes care economy** shape (Part VI): a matching-and-trust marketplace on the full assessment distribution, with a prevention-first safety layer that takes precedence over every other rule.

## 1. Jurisdiction, legal, and compliance review
**Problem.** Mandatory-reporting duties, background-screening requirements, and child-data-protection law vary by jurisdiction and are unresolved.
**Constraints inherited.** The safety track takes precedence over every other rule (Part VI precedent); recording a rating never discharges a legal duty; a safety report must never dead-end in a reputation field.
**Status.** Open. Required before launch; keep current after.

## 2. Background screening — provider and re-screening cadence
**Problem.** Which screening provider, what cadence, what the status signal shows.
**Constraints inherited.** Screening *status*, never report contents, appears as the trust signal; prevention is upstream of reputation because reputation is a lagging indicator (COV-1, COV-2 make harm visible but only after it happens).
**Status.** Open.

## 3. Minors as caregivers
**Problem.** Whether teen babysitters are permitted, and under what regime.
**Constraints inherited.** A minor caregiver is themselves a protected party: guardian consent, no adult-style exposure, youth-labour compliance. This never falls out of the generic adult flow.
**Status.** Open; default off until deliberately decided.

## 4. Trust/safety team and escalation runbook
**Problem.** Staffing, hours, and the concrete workflow behind the safety track.
**Constraints inherited.** The safety track is independent of reputation; an automated or analytic flag is an input to human review, never a finding (the contestable-flag posture).
**Status.** Open.

## 5. Payments and escrow
**Problem.** Payment handling, escrow/dispute mechanics, how agreed price ties to the `+1` definition.
**Constraints inherited.** Settlement begins as pre-funded escrow (the escrow phase); any later move toward credit is a governed configuration change behind Board approval, membership notice, and a completed regulatory review (ECO-5, and bylaws §5.7); credit would be earned, never bought, never redeemable (ECO-4).
**Status.** Open; escrow-first is the committed default.

## 6. Dispute and right-of-response for −1 ratings
**Problem.** The contest path for a `-1` that does not rise to a safety incident.
**Constraints inherited.** The covenant is symmetric — every claim is answerable and a rated party with no answer is a symmetry breach (COV-3); dismissals are annotations, never erasures (REC-2). The safety track may override the covenant in the interim, but due process governs the *durability* of consequences.
**Status.** Open. Until resolved, CTN carries a known symmetry gap.

## 7. Record-layer inheritance
**Problem.** CTN stores immutable rating events but does not yet bind to the witnessed record — no per-operator log, no signed checkpoints, no independent witnesses.
**Constraints inherited.** Append-only, corrections as new entries (REC-1); no child PII in anything anchored or shared — child data never leaves the access-controlled engagement record (REC-3); until two or more independent witnesses exist, any conduct evidence is self-attested and every disposition must say so (architecture open problem 2).
**Status.** Open. Inherit from the built record instances when CTN reaches build.

## 8. Relation typing
**Problem.** CTN has rating categories but no mapping onto the record's relation types (trade, adjudication-conduct, verdict-satisfaction).
**Constraints inherited.** Ratings and claims carry a relation type and no reader collapses them into one figure (REC-9) — that is the forbidden average committed across relations.
**Status.** Open — map categories onto typed relations at build time.
