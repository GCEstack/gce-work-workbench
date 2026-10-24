# GCE Side Hustle Gigs — Validation-First Product Architecture

**Status:** Technical vision / requirements candidate, **NOT an implemented system**.  
**As of:** 2026-10-24.  
**Project owner:** User; builder assignments are tentative.  
**Target repository:** `GCEstack/GCE_Side_Hustle_Gigs` **not found via connected GitHub as of review**. This document lives in the existing workbench pending a project repository.  
**Purpose:** Help an individual find legitimate paid research/testing/AI-evaluation opportunities, manage applications and due dates, and reconcile actual earnings, without violating account/platform rules.

## The fundamental correction

The initial handoff contains good product goals but conflates **source availability**, **legal/authorized collection method**, **alert latency**, **opportunity value**, and **medical eligibility**. None of the example sender domains, inboxes, third-party APIs, refresh intervals, salary estimates, or plasma rules should be treated as verified configuration.

The architecture should treat a platform's **capability as a tested property**. If a platform has no approved API/notification feed, its connector must be `MANUAL_ONLY` or `EMAIL_NOTIFICATIONS_ONLY`, not a speculative scraper.

### P0 validation blockers

| Assumption in original handoff | Current assessment | Required correction |
| --- | --- | --- |
| Proton Mail is the universal primary hub | **Not validated.** Proton Bridge requires a paid plan and a continuously running desktop-side Bridge process. | Support Gmail/Outlook/Proton as distinct sources. Proton is an optional adapter after account/Bridge proof. Do not require mail forwarding to operate. |
| Proton has a general consumer API for mail polling | **Unverified.** | No `Proton API` adapter until a documented supported route is established; Bridge IMAP is a local adapter only. |
| Forward everything from Outlook/Gmail to Proton | **Not required and may leak sensitive mail or duplicate events.** | Start with direct authorized reads or narrow opt-in rules, avoid forwarding entire messages by default; never forward customer test content. |
| Sender email domain identifies the platform | **Fragile and spoofable; examples are not authoritative.** | User-configured sender rules plus authentication/trust signals where available, allowlists, link allowlisting, deduplication, and manual confirmation. |
| Scrape all dashboards on a fixed interval | **Not approved.** Platform terms and rate limits may prohibit bots/automated collection. | Each source requires a documented permissions/capabilities check and safe mode. No browser automation against participant dashboards before explicit authorization by source. |
| Prolific API / frequent study polling | **Unsafe assumption.** Prolific warns against automated scripts and rate-limit triggering behavior. | Use official participant notifications/Assistant and manually logged studies; no automated study reservation or polling. |
| Two-minute alerts for all new tasks | **Cannot be guaranteed if a source only emails intermittently, or service is offline.** | SLA measured from **event observed by the system**, not actual undisclosed platform posting time; measure p50/p95 latency, misses and adapter health. |
| Plasma is eligible at +48 hours | **Incomplete**: U.S. guidance also limits frequency to twice per rolling 7-day window and provider/clinician screening still governs. | Software shows an **earliest planning window only**, after checking both interval and rolling count; never marks donor medically eligible or books over a center's rules. |
| Earnings estimate is income | **Incorrect.** | Separate advertised amount, offered amount, accepted payout, pending, paid, fees, and effective hourly rate including screeners/unpaid time. |
| Five-day build schedule | **Unsubstantiated.** | Use acceptance gates and staged delivery, not day-based promises. |
| Config includes personal emails/tokens | **Unsafe for source control.** | Secrets via environment/OS keychain, local encrypted store or vault; use placeholders; no personal mail addresses in committed files. |

## Operational constraints and platform behavior

**Proton Bridge:** Desktop local IMAP/SMTP access requires a paid Proton Mail plan; Bridge must be running. It is not a hosted public API. Source: https://proton.me/support/imap-smtp-and-pop3-setup

**Prolific:** Automated frequent requests can trigger rate limits; Prolific expressly prohibits automation that reserves studies and directs participants to official Assistant tooling. Source: https://participant-help.prolific.com/en/articles/726488-429-too-many-requests-errors

**UserTesting:** Contributor rules restrict some platform use, forbid AI-generated content during tests, and impose confidentiality conditions. Scraping/copying platform UI/data needs terms-specific review; **do not implement a Playwright poller as an assumed entitlement**. Sources: https://www.usertesting.com/privacy-center/terms-of-service-contributor and https://support.usertesting.com/hc/en-us/articles/4405136672403-Contributor-Code-of-Conduct

**Plasma:** U.S. source-plasma frequency is generally no more than twice per seven-day period and no more than once per two-day period (subject to specific calendar-day exceptions, screening and center rules). Do not implement a simplistic universal `donation_date + 48 hours` eligibility determination. Sources: https://www.hhs.gov/oidp/topics/blood-tissue-safety/giving-plasma/index.html and https://www.fda.gov/inspections-compliance-enforcement-and-criminal-investigations/inspection-guides/section-2

**Calendar:** An iCal subscription and an editable two-way sync are different things. Google/Outlook sync rules require explicit ownership, direction and conflict resolution. Sources: https://support.google.com/calendar/answer/37648 and https://support.microsoft.com/en-us/outlook/calendar/see-your-google-calendar-in-outlook

## Validated product intent vs implementation hypotheses

### P0 — Buildable initial product

1. **Opportunity inbox:** Ingest explicitly authorized notification emails from already-connected mail accounts or manually pasted opportunity URLs; allow user labeling and correction.
2. **Normalized task ledger:** Source, source-native ID (when known), URL, discovery time, original message ID, task category, deadline, advertised pay, screening/eligibility notes, confidence, and `observability_state`.
3. **Deduplication:** Stable identity derived from provider + native task ID; fallback canonical URL/message ID + bounded fingerprint; record merges as reversible provenance links.
4. **Activity state machine:** `observed → needs_review → opened → applied → accepted → in_progress → submitted → approved → paid`; with `expired, rejected, canceled` as terminal outcomes where appropriate. Never treat `discovered` as `available_to_me` without proof.
5. **Local dashboard:** Sorted/filterable actionable feed, source health, manual mark/reconciliation, earnings views; expose last refresh time and what could not be checked.
6. **Notification pipeline:** Push for *new high-priority observed* opportunities with opt-in, idempotent alerts, quiet hours, retries and per-source alert latency. No one-click account actions except opening an official URL.

### P1 — Once P0 proven

- Calendar reminders and deadline tracking with explicit permissions, source/calendar dedupe and daylight-saving-aware timestamps.
- Donation appointment and interval planning (not medical clearance): store actual donation history; flag when scheduling would conflict with the center's stated rules, never assert eligibility.
- Earnings audit: expected vs approved vs transferred amounts, platform-specific currencies, fees and hours invested; payments are user-confirmed or verified via an authorized source.
- Source-specific adapters that have written verification for access methods and permitted automation.
- Offline/reconnect durability; replay, retries and no-loss ingestion history.

### P2 — Conditional

- Browser automation only where explicit published terms or written approval permit it; never automatically reserve studies, answer screeners, scrape confidential study material or bypass anti-bot protections.
- Additional provider onboarding with a `provider_capabilities.yaml`-style declaration, **no hard-coded providers or assumed sender addresses**.
- Productization only after data-protection, terms, support and licensing review.

## Architecture (portable, source-neutral)

```text
Sources (IMAP/connected mail/manual import/permitted provider API)
  → Adapter capability gate: permitted? configured? healthy?
  → Immutable ingestion event (source, received_at, provenance)
  → Classification + trust and link checks
  → Opportunity normalization + confidence/missingness
  → Dedupe and canonical opportunity ledger
  → User-visible task state machine
  → Alert decision engine (priority, consent, quiet hours)
  → Notification delivery record + retries
  → Dashboard and reporting
  → Calendar planner / earnings reconciliation (later)
```

**Rule: MISSING ≠ ZERO; UNOBSERVED ≠ NONE AVAILABLE; ESTIMATE ≠ PAID; NOTIFIED ≠ DELIVERED; PLANNING WINDOW ≠ MEDICAL ELIGIBILITY.**

## Provider capability registry instead of hard-coded scrapers

Each provider entry should declare:
- `provider_id`, display name, official base URL, verified date, owner;
- channels: `email`, `manual`, `documented_api`, `official_extension` (informational only), `browser` (disabled until approved);
- authorization status and link to evidence;
- rate limits and allowed polling interval **only after proven**;
- supported opportunity fields and confidence;
- last observed notification, last successful check, error state;
- restrictions: `no_auto_reservation`, `no_screeners`, `no_study_material`.

**Initial candidates, not preapproved adapters:** UserTesting, CloudResearch Connect, Prolific, Survey Junkie, G2i, Surge AI, Respondent and donation centers. Add/remove providers by configuration and recorded permissions, not by source-code branching.

## Preferred stack decision

**MVP:** Python 3.11+, FastAPI or Flask (**choose one after repository/runtime inspection**), SQLite with WAL and migrations, SQLAlchemy or equivalent, Pydantic/typed settings if FastAPI, background scheduler with single-instance lock and durable last-success checkpoints, responsive plain HTML or minimal React **only if the interface earns its complexity**.

**Mail:** Supported connected-source fetch or local Bridge IMAP. Least-privilege OAuth/scoped credentials where possible. Keep credentials out of config committed to Git and logs.

**Alerts:** Opt-in ntfy/Pushover with authenticated/private channels; public ntfy topics are not appropriate for opportunity details unless access controlled. Avoid assuming a particular vendor/package name is an official client library.

**Deploy:** Local-first while Bridge is needed; a cloud server cannot transparently reach `127.0.0.1` on the user's laptop. Cloud hosting requires a different mail ingestion route and secure device-to-cloud boundary.

**Dependencies:** Pin from freshly supported versions after build-time verification. Remove `sqlite3` from pip dependencies (Python standard library). Do not blindly use 2023-era pinned frameworks.

## Data model: design contract, not final migrations

- `source_accounts`: owner, provider, adapter type, auth reference, enabled, verified capabilities, last checked, permission status.
- `ingestion_events`: immutable IDs, source UID, timestamps (UTC), summary metadata, payload hash and retention policy.
- `opportunities`: canonical ID, provider ID, source ID/URL, title, category, pay min/max + currency, estimate basis, required time, source observed timestamp, deadline, uncertainty.
- `opportunity_events`: status transitions, actor, reason, linked source event.
- `notifications`: opportunity ID, channel, priority, created/attempted/delivered timestamps, idempotency key, failure reason.
- `work_sessions`: task ID, user-recorded minutes, submitted state, actual hours.
- `earnings`: linked task, gross/fees/net, expected/approved/paid, currency, dated payout, evidence type.
- `appointments`: calendar/event ID, type, scheduled/actual time, location, user confirmation.
- `donation_records`: timestamp, center, user-confirmed event, next *planning* date, center restrictions, screening disclaimer.

Never store entire sensitive email bodies or gig test/customer artifacts by default.

## Ranking: explicitly provisional

Use estimated **net compensation / total time**, where total time includes screening, preparation, task execution, payment/admin, and expected unpaid time. Unknown time/pay yields **INSUFFICIENT_EVIDENCE**, not zero or artificially low urgency. Combine user-configurable weights for deadline pressure, fit, payout certainty, travel costs, and elapsed availability. Show the reason and factors, never an unexplained rank.

Do not hardcode “urgent = UserTesting,” “high = Prolific > $10” or “all gigs above $15/hr”; those are optional user-adjustable policies, with provider-normalized currency/time.

## Acceptance tests that can actually be measured

| Gate | Pass condition |
| --- | --- |
| Mail intake | In seeded integration tests, 100% of authorized test messages are either ingested once or quarantined with a visible reason. No duplicates on replay. |
| Source state | Dashboard distinguishes last checked, unknown, unavailable, and no new events. Disabled sources are visibly excluded. |
| Alert latency | **Target**: p95 less than 2 minutes **from successful event ingestion to notification provider acceptance** for connected working services. Not a guaranteed latency from platform publication or phone delivery. |
| Secret handling | No personal addresses, tokens, Bridge passwords, message bodies or test data in Git, logs, alert URLs or error telemetry. |
| Provider policy | No code path performs browser scraping/reservations for sources lacking recorded permission. |
| Earnings | Expected, pending, approved and paid are distinct; reversible correction/traceability; no invented payout. |
| Calendar | No event is written or duplicated absent explicit integration authorization; retries are idempotent. |
| Donation | Flags 48h/twice-in-seven-day constraints as scheduling heuristics, center-specific exceptions, screening and authorization; never claims medical eligibility. |
| Reliability | Network outage, expired token, invalid sender, replay, daylight-saving change and restart do not silently lose state. |

A “zero missed opportunities over 7 days” claim is **not testable** if sources offer no independent complete truth feed. Replace with an instrumented **observed-event delivery rate** and explicitly list non-observable channels.

## Build gates, not a fictitious five-day promise

**Gate A — Evidence:** Verify account access, plan, permissions, platform policy, actual notification examples, allowed read methods and hosting location.  
**Gate B — Offline MVP:** Seeded fake messages/manual links → canonical ledger → dashboard → test alerts; integration tests.  
**Gate C — Live authorized mail:** One approved account/adapter with host-side audit and dedupe.  
**Gate D — Alerts + earnings:** User-tested phone delivery, audit of accepted and paid work, latency metrics.  
**Gate E — Calendar and donation planner:** Scoped calendars, user confirmation and donor-center scheduling constraints.  
**Gate F — Expansion/productization:** Provider-by-provider authorization, privacy, commercial terms and cost evidence.

## Unresolved questions recorded as requirements, not blockers to writing this design

- Which mail services and subscriptions are already available? Is Proton Bridge operational on an always-on host?
- Which platforms send usable opt-in notification emails and which prohibit automation?
- What is the priority: additional income quickly, low administration burden, minimum financial overhead, or broad provider coverage?
- Is the software local-only, personally hosted, or intended for multiuser commercial release?
- Which calendar should be the write-owning source of truth? Is Outlook sync required or only read-only context?
- Which plasma center policies apply? A center and qualified screening staff decide donor eligibility, not this app.

## Publication and ownership boundary

This document is safe to discuss as a **proposed engineering architecture**, not evidence of a shipped app. Any private email, payout, medical/donation or account details must live outside public repositories.

## Sources validated 2026-10-24

- Proton Bridge paid/local limitation: https://proton.me/support/imap-smtp-and-pop3-setup
- Prolific automation and rate limits: https://participant-help.prolific.com/en/articles/726488-429-too-many-requests-errors
- UserTesting contributor terms: https://www.usertesting.com/privacy-center/terms-of-service-contributor
- UserTesting contributor code: https://support.usertesting.com/hc/en-us/articles/4405136672403-Contributor-Code-of-Conduct
- HHS plasma donation overview: https://www.hhs.gov/oidp/topics/blood-tissue-safety/giving-plasma/index.html
- FDA plasma collection frequency: https://www.fda.gov/inspections-compliance-enforcement-and-criminal-investigations/inspection-guides/section-2
- Calendar interoperability: https://support.google.com/calendar/answer/37648

