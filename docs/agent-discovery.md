# SafeGen visiting-agent discovery status

**Updated:** 10 October 2026 (Australia/Sydney)  
**Owner:** Sam, SafeGen manager (Linear RIC-226 / RIC-78)  
**Purpose:** Truthful public inventory so a cold agent can find what exists **without private guidance**, and can tell its human what is still broken.

This page prefers truth over theatre. It does **not** claim October 4 launch acceptance.

## Gate summary (RIC-78)

| Gate | Status |
|---|---|
| 1. Machine-readable capabilities, auth, limits, schemas, sandbox instructions published where a visiting agent can find them without private guidance | **Partial / unmet on production hosts** — this docs repo now publishes `llms.txt` + `agent.json` + this page; brand/app still lack OpenAPI / well-known / MCP |
| 2. Unfamiliar agent can discover the service, run a capped synthetic example, and explain the result without private guidance | **Partial** — the capped synthetic evaluation kit is now public and MIT-licensed at https://github.com/RicRicho/safegen-evaluation-kit (release v0.1.0). It runs on loopback fixtures only. A cold-agent test against these public pages is still to be recorded. Live `POST /api/check` is not that sandbox |
| 3. Human/organisation sponsorship path documented | **Partial** — brand contact + Platform API Pack request forms exist; no self-service path to test/production credentials (RIC-76) |

## Live surfaces (fresh probes 30 Sep 2026)

### Brand — `https://www.safegen.com.au`

| URL | Result | Cold-agent useful? |
|---|---|---|
| `/` | 200 marketing homepage | Human marketing only |
| `/platforms`, `/platforms/api`, `/contact`, `/about`, audience pages | 200 | Pitch + EOI forms; **not** credentials |
| `/llms.txt`, `/.well-known/*`, `/openapi.json`, `/docs`, `/developers`, `/api/*`, `/check*`, `/enrol` | 404 (HTML) | No |
| Live Demo link → `https://demo.safegen.com.au/` | 200 tiny SPA stub (stale) | Not a usable API/docs surface |

### App — `https://child-social-media-check.vercel.app`

| URL | Result | Cold-agent useful? |
|---|---|---|
| `/` | 200 app shell; links to check/enrol/api-docs | Navigation only |
| `/api-docs` | 200 **human HTML** describing `POST /api/check` | Partial — readable, not machine schema |
| `POST /api/check` | 200 JSON safelist probe (`listed`, `blockRequested`, `action`, `checkedAt`) | Partial — callable, but **not** capped synthetic sandbox; no auth gate today |
| `GET /api/stats` | 200 JSON with null/unverified counters | Not acceptance evidence |
| `/check-number`, `/enrol` | 200 UI fail-closed (“service is not connected” / enrolment unavailable) | Explains unavailability correctly |
| `/api/check-number`, `/api/enrol` | 404 | No |
| `/llms.txt`, OpenAPI, MCP, agent cards, `/developers`, `/signup` | 404 | No |

### Public repos / pages

| Surface | Notes |
|---|---|
| https://github.com/RicRicho/safegen-docs + GitHub Pages | Public concept docs + **this discovery pack** |
| https://github.com/RicRicho/safegen-v4 | Design/architecture notes; not the running app |
| https://github.com/RicRicho/safegen-evaluation-kit | **Public, MIT** synthetic evaluation kit `@safegen/evaluation-kit` 0.1.0 (loopback fixtures only) |
| https://github.com/RicRicho/safegen-v3 | **Private** app repo |
| https://safegen.gitbook.io/press-kit/ | Press kit |

## Synthetic example path (public)

The capped loopback synthetic evaluation kit `@safegen/evaluation-kit` 0.1.0 is public under the MIT licence:

- Repo: https://github.com/RicRicho/safegen-evaluation-kit
- Release tarball: https://github.com/RicRicho/safegen-evaluation-kit/releases/tag/v0.1.0

Run it without any private access:

```sh
git clone https://github.com/RicRicho/safegen-evaluation-kit.git
cd safegen-evaluation-kit
node --test test.mjs   # expect 12/12 pass
node example.mjs       # prints match / no-match / no-block / unknown / error decisions
```

What it shows: how a platform should read a SafeGen check result. `match` with a block request means reject; `no_match` or a match without a block request means carry on with your other checks; `unknown` or `error` means hold for retry or review (fail closed). The sandbox binds only to `127.0.0.1`, uses fixture phone numbers only, has a lifetime quota of 30 requests and a 1 KiB body limit, and makes no calls to SafeGen, Twilio or any social platform.

Verified 10 Oct 2026 (Sydney) from a clean public clone: 12/12 tests pass and the example prints all five fixture decisions.

What it does **not** show: real-service or real-phone behaviour, or launch readiness.

**Do not substitute** live `POST /api/check` for the capped synthetic sandbox. That route is a live safelist membership probe.

## Sponsorship / human org onboarding

Documented today:

1. https://www.safegen.com.au/contact — structured EOI form to “SafeGen Standards Team”
2. https://www.safegen.com.au/platforms/api — “Request Platform API Pack” form (docs/examples/compliance materials request)

**Not documented / not working as acceptance requires:**

- Self-service integration-account creation
- Immediate test credentials
- Documented usable path to authorised production credentials
- Machine-readable auth/limits for production checks

Tracked as **RIC-76**. A request form alone is explicitly insufficient for that ticket.

## Next steps (no wait on Ric)

1. Keep this discovery pack accurate as RIC-76/77 move.
2. Link the public kit from the app's `/api-docs` page as well (app changes follow the current live-site hold).
3. Record a cold visiting-agent run that starts from these public pages only.
4. Add production-host `llms.txt` / OpenAPI / agent card **only** when they describe real working routes (no fake green).
5. Wire brand/app discovery links to this docs pack once ready.
6. Keep check/enrol fail-closed until real-phone evidence exists.

## Dependencies

- **RIC-76** — platform + developer self-service signup / credentials
- **RIC-77** — developer kit with working example (public kit released 30 Sep 2026)
- Coordinates under **RIC-226** (Sam delivery owner since 7 Oct 2026). Jenny hibernated — do not assign her.
