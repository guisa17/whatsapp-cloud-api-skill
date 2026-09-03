# Changelog

All notable changes to this skill are documented here.

Because this skill describes a third-party platform that changes without
notice, **each release records what was verified and when**. A stale skill is
worse than no skill — it sends you down the wrong path with confidence — so
the verification date is treated as content, not metadata.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [1.1.0] — 2026-09-03

Re-verified against Meta's documentation, and added field findings from
connecting a real number through Coexistence on 2026-08-31.

### Added

- **Coexistence: Advanced Access is inert while the app is in Development
  mode.** `missing required Graph API permissions for Cloud API companion
  pairing` was raised with all permissions already approved at Advanced Access;
  the actual cause was the app being unpublished. Publishing it to Live fixed
  it with no permission change.
- **Coexistence: Embedded Signup creates its own WABA**, rather than using an
  empty one pre-created and passed to it. This can leave two WABAs with
  near-identical names, one of them invisible to the app — picking the wrong
  one returns only "not a valid business identifier".
- Post-connection guidance: read the WABA ID back from the API instead of
  trusting the one you planned to use, and check `platform_type` is
  `CLOUD_API`.
- The documentation URL restructure: WhatsApp docs moved to
  `/documentation/business-messaging/whatsapp/`, and old `/docs/whatsapp/`
  paths 404 or serve stale copies.
- App Review timing as a single data point: 12 days, approved on first
  submission, against the 20 days Meta's panel advertises.
- Five rows in the symptom→cause table for the above.

### Changed

- The **14-day inactivity rule** moves from `[field]` to `[verified]` — it is
  documented as the `PRIMARY_INACTIVITY` offboarding reason.
- The **Tech Provider** requirement is now stated as Advanced access to *both*
  `whatsapp_business_messaging` and `whatsapp_business_management`.
- The Coexistence path gained a step: `… → Advanced Access → App published
  (Live) → Coexistence`.
- WhatsApp Business app **2.24.17+** requirement added as `[verified]`.
- Flow JSON version-state rules now quote Meta's actual 90-day wording, and
  note that the 12-month support window quoted by third parties is not in
  Meta's docs.

### Verified against Meta's documentation (2026-09-03)

Re-checked; **unchanged since 1.0.0**:

- Graph API is still on **v26.0** (released 2026-07-29).
- Pricing is still **per message** since 2025-07-01; non-template messages and
  utility templates inside an open customer service window are still free.
- Flow JSON versions still freeze, then expire, with ~90 days' notice.

### Not verified this release

- **Latest Flow JSON version.** Meta's Flow JSON changelog returned **HTTP
  500** from every path tried. The `7.3` claim keeps its original
  `2026-08-26` date, and both `SKILL.md` and `README.md` say so rather than
  letting the release date imply otherwise.

### Deliberately not included

- The claim that the free 24-hour service window ends **2026-10-01** remains
  `[unconfirmed]`. Re-checked on 2026-09-03 against both the pricing page and
  the dedicated *Pricing Updates* page: Meta still documents in-window
  non-template messages and utility templates as free, and still attributes
  2026-10-01 only to rate-card changes in nine markets. Third-party accounts
  did get more specific — naming 2026-09-01 as the date Meta would publish
  final service rates — and **that deadline passed with nothing published**, so
  the claim is now marginally weaker, not stronger. §7 says to plan for the
  scenario anyway and re-check Meta directly in late September 2026.
- The **12-month** Flow JSON support window quoted by third-party guides.
  Meta's versioning page states 90 days' notice and no such window.

## [1.0.0] — 2026-08-26

First release. Verified against **Graph API v26.0**.

### Added

- The three invisible steps: WABA→app subscription, webhook field
  subscription, and test-number recipient allowlisting. None of them produce
  an error when missing.
- Token guidance: temporary vs system-user, the two-person approval
  requirement, and why token types are not interchangeable.
- Webhook correctness: raw-body signature validation, constant-time
  comparison, responding 200 before processing, deduplicating by
  `wa_message_id`.
- Flows: publishing by API, version freeze/expiry lifecycle, and the gotchas
  (immutability, empty `data: {}`, `mode` mismatch, unquoted numeric inputs).
- Limits table and pricing model.
- Coexistence and App Review, including the Tech Provider prerequisite.
- Symptom→cause table keyed by Meta error codes.
- `references/diagnose.py`, a standalone diagnostic covering the invisible
  steps and the verification handshake.

### Verified against Meta's documentation

Corrections made while writing, against beliefs that were out of date:

- Pricing has been **per message since 2025-07-01**, not per conversation.
- Flow JSON versions **freeze** and then **expire**; an expired version means
  existing Flows can no longer be opened.
- The **On-Premises API was fully sunset on 2025-10-23**.
- Latest Flow JSON at time of writing: **7.3**.

### Deliberately not included

Widely repeated third-party claims that the free 24-hour service window ends
on 2026-10-01 are **not present in Meta's pricing documentation**. They are
tagged `[unconfirmed]` rather than stated as fact.

[1.1.0]: https://github.com/guisa17/whatsapp-cloud-api-skill/releases/tag/v1.1.0
[1.0.0]: https://github.com/guisa17/whatsapp-cloud-api-skill/releases/tag/v1.0.0
