# CLAUDE.md — Canonical guidance for the Childcare Trust Network (CTN)

> **Working name:** "Childcare Trust Network (CTN)" is a placeholder; rename freely.
> **Status:** Proposal (v0.1.0). Not yet approved for build.
> **Governance substrate:** [LBTAS](https://github.com/NTARI-RAND/Leveson-Based-Trade-Assessment-Scale) ≥ 2.0.0 (the **distribution** model — *no averaging*).

This file is the **source of truth** for working on CTN. When any other document,
code comment, or committed implementation conflicts with this file, this file
wins — treat the conflict as a bug in the other artifact, not here. Read it
before writing or modifying code in this repository.

CTN inherits LBTAS's reputation rules verbatim where they apply, and **adds a
child-safety layer that takes precedence over everything else.** Where a generic
LBTAS rule and a child-safety rule in this document appear to conflict, the
child-safety rule wins. The whole point of a Leveson-derived system is that a
failure is treated as a safety event, not a customer-service blemish — and in
childcare a failure can mean harm to a child. That framing is the spine of this
document.

This proposal assumes the **post-2.0.0** LBTAS behaviour only. Any pre-2.0.0
averaging logic (`system_average`, `category_averages`, per-engagement means,
average-ranked "top/bottom" lists) is explicitly **out of scope and forbidden
here** — see *Do not average*.

## What CTN is

CTN is a childcare matching and trust network. It does two jobs:

1. **A marketplace.** Caregivers publish availability, service types, rates,
   qualifications, and verification status. Parents browse, request, schedule,
   and pay for engagements, and share the information a caregiver needs to care
   for a child safely.
2. **A reputation layer governed by LBTAS.** Completed engagements trigger
   rating prompts. Reputation is a **distribution** of LBTAS ratings (`-1`
   through `+4`) per party, never an average. Harm (`-1`) is surfaced, never
   smoothed away.

CTN is networked, so network use is distribution for licensing purposes (see
*Licensing*), and reads are privileged operations (see *Authorization*).

## The parties — who is rated, and who is never rated

CTN reputation is **multi-directional among adults**:

- **Caregivers** rate **parents/guardians**, and
- **parents/guardians** rate **caregivers**.

A single completed engagement can therefore produce two rating prompts — one in
each direction. (If your model later adds other adult roles, e.g. agency
coordinators, the same rule applies pairwise.)

**Children are never a party and are never a rated subject.** This is
non-negotiable and pervasive:

- A child is never assigned a reputation, never a row in the reputation store,
  never described as a commodity, never browsable, and never the object of a
  rating value.
- Reputation always attaches to the **adult** caregiver or parent account. A
  rating may concern *how a child was cared for during an engagement*, but the
  reputation it produces belongs to the adult, not the child.
- No child name, photo, location, or schedule appears in any public listing,
  profile, or reputation output. Ever. (See *Information sharing*.)

**Minors as caregivers (teen babysitters) is a special case, not a default.** If
CTN ever permits caregivers under the age of majority, those accounts require
guardian involvement and consent, additional protections, no adult-style public
exposure, and compliance with youth-labour and child-safety law in the relevant
jurisdiction. A minor caregiver is themselves a protected party. Treat enabling
this as a deliberate, separately-reviewed decision (see *Open decisions*), not
something that falls out of the generic adult flow.

## Child safety is the first design constraint (non-negotiable)

LBTAS's distribution model surfaces harm *after* it happens. For childcare that
is necessary but **not sufficient** — the first family harmed by a bad actor is
the one that produces the first `-1`, and "the first family" must not be an
acceptable cost. So CTN is **prevention-first**, in the spirit of the LBTAS `+3`
level ("designed to prevent loss"):

**Reputation is a lagging indicator and must never be the only safeguard.**
Front-loaded controls are required before reputation ever comes into play:

- **Identity verification** for every account, required before any first
  in-person engagement.
- **Background screening** for caregivers, appropriate to the jurisdiction, with
  the *status* (not the underlying report contents) reflected as a trust signal.
- **References and, where relevant, certifications** (e.g. first aid / CPR),
  shown as verified attributes, not self-asserted badges.

**A `-1` runs on two independent tracks.** A reputation event is not a substitute
for child protection, and child protection must not depend on whether a harmed
party chooses to leave a rating:

1. *Reputation track.* The `-1` is recorded with its mandatory justifying
   comment (≤500 words), surfaced in `harm_flagged`, and never averaged away.
2. *Safety track.* If a `-1` — or any report, rating or not — describes suspected
   abuse, neglect, exploitation, or imminent danger to a child, it triggers a
   **safety-incident workflow that is independent of reputation**: route to the
   trust/safety team, give the reporter clear guidance to contact local child
   protective services and/or emergency services, preserve records, and consider
   **immediate suspension of the implicated account pending review.** Credible
   risk to a child outweighs fairness-to-the-accused considerations in the
   interim; due process applies to the *durability* of consequences, not to
   whether an at-risk child is protected now.

**This document does not state your legal obligations.** Mandatory-reporting
duties, screening requirements, and data-protection rules vary by jurisdiction
and change over time. Recording a rating does **not** discharge any legal duty.
Get qualified legal/compliance review before launch and keep it current (see
*Open decisions*). The engineering rule that *does* hold everywhere: never build
the system so that a safety report dead-ends in a reputation field.

**No secrecy, no isolation, parental transparency by default.** CTN must never
provide features that facilitate secrecy between a caregiver and a child, or that
isolate a child from their parents/guardians. Coordination is visible to the
responsible parent; communication records exist; the design assumes transparency,
not private side-channels around guardians.

## The assessment scale (inherited from LBTAS)

Ratings are integers from `-1` to `+4`; higher is better. The scale is
**meaning-loaded** — each level carries a specific definition and must not be
treated as an interchangeable point on a continuous axis. CTN keeps the LBTAS
levels and meanings, glossed for childcare:

| Level | Label | LBTAS meaning | Childcare gloss |
|------:|-------|---------------|-----------------|
| +4 | Delight | Anticipates the evolution of user practices and concerns post-transaction | Care anticipates the child's and family's evolving needs; proactive, thoughtful, leaves the family better prepared |
| +3 | No Negative Consequences | Designed to prevent loss; exceeds basic quality | Safety-first care that is designed to prevent harm and exceeds what was asked |
| +2 | Basic Satisfaction | Meets socially acceptable standards beyond articulated demands | Goes beyond the stated job in normal, socially expected ways |
| +1 | Basic Promise | Meets all articulated demands, no more | The agreed scope (and agreed price/schedule) is honoured, nothing beyond |
|  0 | Cynical Satisfaction | Fulfils a basic promise with little to no discipline toward satisfaction | The booking was technically fulfilled with little real care or discipline |
| -1 | No Trust | User was harmed, exploited, or received service with no discipline or malicious intent | **A child or party was harmed, endangered, neglected, or exploited, or the engagement was in bad faith** |

`-1` is the only level that asserts harm or bad faith against another party in
the network, which is why it carries the comment requirement and the safety-track
obligations above.

**Categories.** Like LBTAS, ratings can be filed under categories. Suggested
defaults (tune later):

- *Rating a caregiver:* safety, reliability/punctuality, communication, quality
  of care, professionalism.
- *Rating a parent:* communication, accuracy of the job description, respect and
  safety of the working environment, payment reliability.

One constraint on categories: **no category may penalise a party for protecting a
child.** A parent setting strict rules, requiring check-ins, or limiting what is
shared, and a caregiver refusing an unsafe instruction or escalating a concern,
are *correct* behaviours, not reputation risks.

## Do not average

**Ratings are never averaged.** This is LBTAS's central rule and it is
non-negotiable here. A reputation is a **distribution**: the count of ratings
received at each of the six levels (`-1, 0, +1, +2, +3, +4`) together with the
**total**. There is no `system_average`, no per-category mean, no per-engagement
mean, no average-ranked "top/bottom caregivers", and no "overall rating" field —
not in a return value, not in a report, not in a listing, not in a printed
display.

In childcare the case is even sharper than in generic commerce: averaging lets a
single `-1` — a child who was harmed — be diluted by surrounding praise, so that
a dangerous caregiver presents a comfortable 4.2. That is precisely the failure
mode CTN exists to prevent. The distribution keeps **every `-1` visible**, and
`harm_flagged` raises it explicitly. A mean also compresses away the *shape* (two
parties with very different rating shapes can share one average) and is
dimensionless with respect to count (next section).

**Acceptance bar (inherited from LBTAS):** `grep -iE 'average|mean|system_average'`
finds no averaging logic in any read, report, listing, or display path. A comment
that *explains* the ban is fine.

## The rating count is itself a signal

The `total` for a rated party is not a denominator — it is information. It carries
two things at once: **engagement volume** (how much the party transacts) and a
**proxy for time in service** (a large count generally cannot accumulate without
sustained participation over time). A caregiver with 200 clean ratings over three
years and a brand-new caregiver with five are different parties, and the count is
what distinguishes them. A high total with no `-1`s is a stronger trust signal
than the same clean shape at a low total. Always report the count alongside the
per-level breakdown.

Respect the limits of the proxy. The count is a count of *ratings*, not raw
engagements, and it correlates with longevity without measuring it (a burst of
volume in a short window also produces a high count). Precise volume and tenure
come from the event store: each rating event carries a timestamp and a triggering
**engagement id**, so reads can expose `first_rated_at`, `last_rated_at`, and a
distinct-engagement count beside `total`. Never claim `total` equals engagement
count.

## The -1 comment requirement

A rating of **`-1` must carry a justifying comment of 500 words or less.**

- The comment is **mandatory** for `-1`. Reject any attempt to submit a `-1`
  without one.
- Enforce the **500-word maximum** at the API boundary. Reject submissions that
  exceed it rather than silently truncating.
- For ratings `0` through `+4`, comments are optional unless product requirements
  say otherwise.

A bounded written justification makes the most consequential rating accountable
and reviewable, and gives the safety team the context they need without creating
an unbounded dumping ground. Remember the two-track rule: a `-1` comment that
describes danger to a child is **also** a safety-track trigger, not just a stored
string.

## Reading and reporting reputation — output contract

Reputation attaches to **parties** (caregivers/parents); **engagements**
(bookings) are the triggering events. This is CTN's deliberate reading of the
LBTAS "exchange" term for a multi-party setting — call it out wherever it matters
so it is not mistaken for drift. The LBTAS JSON shapes carry over (key order is
not significant; presence and values are).

`view_ratings(party)` — per-category distribution plus total:

```json
{
  "<category>": {
    "distribution": { "-1": 0, "0": 0, "1": 0, "2": 0, "3": 0, "4": 0 },
    "total": 0
  }
}
```

`generate_report()` — overall, per-category, and per-party distributions plus the
harm list:

```json
{
  "total_engagements": 0,
  "total_ratings": 0,
  "overall_distribution":   { "-1": 0, "0": 0, "1": 0, "2": 0, "3": 0, "4": 0 },
  "category_distributions": { "<category>": { "-1": 0, "0": 0, "1": 0, "2": 0, "3": 0, "4": 0 } },
  "party_distributions":    { "<party>": { "distribution": { "...": 0 }, "total": 0 } },
  "harm_flagged": [ ["<party>", 0] ],
  "generated_at": "ISO-8601"
}
```

- `harm_flagged` lists every party that received one or more `-1` ratings, sorted
  by `-1` count descending (ties broken by name ascending for stable output).
- **Display order** for printed distributions is best-to-worst (`+4` down to
  `-1`), one line per level: `level  label : count`.
- Listings show the total number of ratings per party and append a harm flag
  (e.g. `, 3x -1 No Trust`) when the party has any `-1`. They show **no average**.
- Reads label the total explicitly as engagement volume
  (`Total ratings (engagement volume): N`) and surface `first_rated_at` /
  `last_rated_at` as an "in service since / last active" range.
- Interactive/demo output prints counts, never an average.

## Platform capabilities

### Availability and pricing listings
Caregivers publish time slots, service types, rates, location radius, and
qualifications. The listing shows **verification status, the LBTAS distribution,
and tenure** — three honest signals, never collapsed into one score. Verification
and certification claims must be substantiated by the platform; self-asserted
badges are not shown as verified.

### Hiring and scheduling
Parents browse, request, and book; engagements require **mutual confirmation**.
Booking creates the **engagement id** that later ties rating prompts (reputation
track) and the scoped child-information share (data track) to the same event.
Identity verification is required before the first in-person engagement. Capture
clear check-in/out, cancellation rules, and emergency contacts. The agreed price
and scope are part of the engagement record; honouring them is what a `+1`
("basic promise") means.

### Information sharing — child data (minimise and scope hard)
Parents share what a caregiver needs (allergies, medical needs, routines,
emergency contacts, pickup authorisation). This is sensitive child data and is
governed by strict rules:

- **Data minimisation.** Collect the least information needed for a specific
  engagement.
- **Purpose limitation and access scoping.** Child information is visible only to
  the specific caregiver booked for that engagement, only for its duration, and
  to the responsible parent. Access ends when the engagement ends.
- **No public child data.** No child names, photos, schedules, or locations in
  listings, profiles, or any reputation output.
- **No secondary use.** Child data is never used for ranking, advertising, model
  training, or any purpose beyond delivering that engagement's care.
- **Security and retention.** Encrypt in transit and at rest; log access; define
  and enforce a retention/deletion policy; let parents revoke shares.
- **Separation from reputation.** Child data lives in the access-controlled
  engagement record, **never in the reputation/event store**, and is never an
  input to a reputation computation.

### Communication and records
In-app messaging keeps an audit trail that supports accountability, dispute
resolution, and the no-secrecy principle. Records are retained per policy,
available to authorized reviewers, and never public.

## Data model — the event store (and what must stay out of it)

Because reputation is a distribution and `-1`s carry comments, the store keeps
**individual rating events**, not running tallies. Each event captures at least:

- the **rated party** (an adult — caregiver or parent),
- the **rater** (an adult; multi-directional),
- the **rating value** (`-1`..`+4`),
- the **category**, if in use,
- the **comment** (required when value is `-1`, ≤500 words),
- a **timestamp**,
- the **triggering engagement id**,
- a **safety-incident flag** routing to the safety track when set.

Distributions are computed from these events on read; the events are the audit
trail. Reads expose `first_rated_at`, `last_rated_at`, and a distinct-engagement
count beside `total`.

**What the event store must never contain:** any child PII. Rating events concern
adult reputation only. Child information stays in the separate, access-controlled
engagement record and is never used to compute reputation.

## Authorization

Reading records is a privileged operation. Implement an explicit authorization
layer between callers and the stores, and treat these as **distinct capabilities,
authorized separately**:

1. submitting a rating in response to a served prompt,
2. reading reputation records,
3. reading the child information shared for an engagement,
4. performing safety-team review and escalation.

**Fail closed.** An unauthenticated or unauthorized caller reads nothing. Child-
information access is the most tightly scoped of all: the booked caregiver for the
engagement window only, the responsible parent for their own children, and the
safety team only under audited conditions.

## Versioning

CTN is at **0.1.0** (proposal stage). It depends on **LBTAS ≥ 2.0.0** (the
distribution model); pre-2.0.0 averaging behaviour is out of scope. When code
lands, keep every version string in sync on each bump, following the LBTAS
convention across language implementations.

## Licensing

The project is **AGPL-3.0** — the GNU **Affero** General Public License v3.0, not
the plain GPL v3 — consistent with LBTAS. Network use counts as distribution,
which is the relevant case for a networked platform, so AGPL-3.0 wins any conflict
with stray `GPL-3.0` strings. Every source file should declare AGPL-3.0, and the
`LICENSE` file must be the full AGPL-3.0 text.

## Open decisions (resolve before build)

> **Canonical home:** these decisions now live in [`OPEN-QUESTIONS.md`](./OPEN-QUESTIONS.md) — the living open-questions deliverable required by Janus-Facing Architecture — with the constraints each resolution inherits. Update there; this list is a summary.

These are genuine product/legal choices this proposal does **not** settle:

- **Jurisdiction and legal/compliance review** — mandatory-reporting duties,
  background-screening requirements, and child-data-protection law. Required
  before launch; keep current.
- **Background-screening provider and re-screening cadence.**
- **Age ranges of children served**, and whether **minors may be caregivers** (if
  yes, the guardian-consent and protection regime in *The parties*).
- **Trust/safety team** — staffing, hours, and the concrete escalation runbook
  behind the safety track.
- **Payments** — handling, escrow/dispute mechanics, and how agreed price ties to
  the `+1` definition.
- **Dispute and right-of-response process** for `-1` ratings that do *not* rise to
  a safety incident, balanced against child protection for those that do.

## Contact

Network Theory Applied Research Institute — info@ntari.org
