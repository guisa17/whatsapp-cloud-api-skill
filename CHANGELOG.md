# Changelog

All notable changes to this skill are documented here.

Because this skill describes a third-party platform that changes without
notice, **each release records what was verified and when**. A stale skill is
worse than no skill — it sends you down the wrong path with confidence — so
the verification date is treated as content, not metadata.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

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

[1.0.0]: https://github.com/guisa17/whatsapp-cloud-api-skill/releases/tag/v1.0.0
