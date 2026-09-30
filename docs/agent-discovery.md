# SafeGen visiting-agent discovery status

**Updated:** 30 September 2026 (Australia/Sydney)  
**Owner:** Max (Linear RIC-226 / RIC-78)  
**Purpose:** Truthful public inventory so a cold agent can find what exists **without private guidance**, and can tell its human what is still broken.

This page prefers truth over theatre. It does **not** claim October 4 launch acceptance.

## Gate summary (RIC-78)

| Gate | Status |
|---|---|
| 1. Machine-readable capabilities, auth, limits, schemas, sandbox instructions published where a visiting agent can find them without private guidance | **Partial / unmet on production hosts** — this docs repo now publishes `llms.txt` + `agent.json` + this page; brand/app still lack OpenAPI / well-known / MCP |
| 2. Unfamiliar agent can discover the service, run a capped synthetic example, and explain the result without private guidance | **Unmet** — capped synthetic kit is private/UNLICENSED on `RicRicho/safegen-v3` PR7; not publicly installable. Live `POST /api/check` is not that sandbox |
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
| https://github.com/RicRicho/safegen-v3 | **Private** app repo; PR7 kit not public |
| https://safegen.gitbook.io/press-kit/ | Press kit |

## Synthetic example path (attempted)

**Public cold path:** FAIL for RIC-78 gate 2.

Exact blocker: the capped loopback synthetic evaluation kit (`@safegen/evaluation-kit` 0.1.0) lives on private branch `codex/sdk-evaluation-kit` / [PR7](https://github.com/RicRicho/safegen-v3/pull/7), package `private:true` / `UNLICENSED`. A visiting agent without private GitHub access cannot install or run it from public docs alone.

**Authenticated Max verification (not cold-agent proof):** downloaded PR7 `sdk/` and ran locally on 30 Sep 2026:

- `node example.mjs` — match / no-match / no-block / unknown / error fixtures printed as expected
- `node --test test.mjs` — **9/9 pass**
- Sandbox is loopback-only, fixture phones only, default quota 30 requests

This proves the kit exists for owners; it does **not** satisfy “without private guidance”.

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

## What Max can do next without waiting on Ric

1. Keep this discovery pack accurate as RIC-76/77 move.
2. After RIC-77 publishes a licensed public kit: add install URL + sandbox instructions here and on app `/api-docs`.
3. Add production-host `llms.txt` / OpenAPI / agent card **only** when they describe real working routes (no fake green).
4. Wire brand/app discovery links to this docs pack once ready.
5. Do not reopen fail-closed check/enrol until RIC-81 evidence exists.

## Dependencies

- **RIC-76** — platform + developer self-service signup / credentials
- **RIC-77** — publish developer kit with working example (due 2026-10-04)
- Coordinates under **RIC-226** (Max delivery owner). Jenny hibernated — do not assign her.
