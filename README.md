# WhatsApp Cloud API — Claude Skill

Field notes for building bots on Meta's WhatsApp Cloud API, packaged as a
[Claude Code skill](https://docs.claude.com/en/docs/claude-code/skills).

**The premise:** in this API, the default failure mode is silence. The three
most common misconfigurations produce no error, no warning, and no failed
request — the panel reports "connected successfully" and messages simply never
arrive. Most of this document is about those.

## Install

```bash
git clone https://github.com/YOUR-USER/whatsapp-cloud-api-skill.git \
  ~/.claude/skills/whatsapp-cloud-api
```

Claude picks it up automatically. Invoke it with `/whatsapp-cloud-api`, or just
describe a Cloud API problem and it will load on its own.

For a single project instead of your whole account, clone into
`<project>/.claude/skills/` .

## What's inside

| File | |
|---|---|
| [`SKILL.md`](SKILL.md) | The knowledge. Tokens, webhooks, Flows, limits, pricing, Coexistence, and a symptom→cause table |
| [`references/diagnose.py`](references/diagnose.py) | Standalone diagnostic. Checks the three invisible steps and the verification handshake |

### The diagnostic

Copy it into a new project **before** writing bot logic — it's the
highest-leverage thing you can build, and you want it before you need it.

```bash
export WHATSAPP_TOKEN=...
export WHATSAPP_PHONE_NUMBER_ID=...
export WHATSAPP_WABA_ID=...
export WHATSAPP_APP_SECRET=...      # optional, to check webhook fields
export WHATSAPP_VERIFY_TOKEN=...    # optional, to test the handshake
export WEBHOOK_URL=...              # optional, to test the handshake

python references/diagnose.py        # report only
python references/diagnose.py --fix  # also fix what can be automated
```

Only dependency is `httpx`.

## How claims are tagged

Not everything here carries the same weight, so each claim says where it comes
from:

- **[verified]** — confirmed against Meta's documentation or a live API call.
- **[field]** — observed in production. True at least once, for at least one setup.
- **[unconfirmed]** — reported by third parties and *not* found in Meta's docs.
  Verify before acting on it.

**Last verified: 2026-08-26, against Graph API v26.0.**

## The freshness problem

Meta redesigns its panels often, and **a stale skill is worse than no skill** —
it sends you down the wrong path with confidence. Two consequences:

- Anything describing *where a button lives* is the first thing to age. The
  skill says so, and tells you to identify screens by their content instead.
- The `last-verified` date at the top of `SKILL.md` is part of the content, not
  metadata. If you update something, move it.

## Contributing

This comes from a small number of production deployments, so the sample size
behind any **[field]** claim is, by definition, small. If something is wrong,
out of date, or missing a case you hit, please open an issue — especially:

- Panel navigation that has changed
- Error codes not in the symptom→cause table
- Anything tagged **[field]** that turned out to be specific to one setup
- Anything tagged **[unconfirmed]** that you can confirm or refute

## License

MIT. See [LICENSE](LICENSE).
