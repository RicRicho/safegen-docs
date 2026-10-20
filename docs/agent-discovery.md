# SafeGen for visiting agents

**Updated:** 20 October 2026 (Australia/Sydney)
**Owner:** Sam, SafeGen manager (Linear RIC-78, RIC-226)

SafeGen runs a Do Not Connect register of Australian children's phone numbers. Platforms ask SafeGen whether a phone number belongs to a registered child before letting it open or link an account. Raw numbers are never stored.

## Start here

| What | Where |
|---|---|
| Live website | https://www.safegen.com.au/ |
| API reference (human page) | https://www.safegen.com.au/api-docs |
| Create a test account and get a test key at once | https://www.safegen.com.au/developers/sign-up |
| Machine-readable summary | https://ricricho.github.io/safegen-docs/agent.json |
| Plain-text index | https://ricricho.github.io/safegen-docs/llms.txt |
| Offline practice kit (MIT, no network) | https://github.com/RicRicho/safegen-evaluation-kit |

## 1. Get a test key

```sh
curl -s -X POST https://www.safegen.com.au/api/integrations/signup \
  -H 'content-type: application/json' \
  -d '{"orgName":"Your org","contactName":"Your name","contactEmail":"you@example.com","website":"https://example.com"}'
```

Returns `201` with `accountId`, `testApiKey` (shown once only, store it), `rateLimitPerHour` (60) and the list of practice values. Signing up again with the same email returns `409`.

## 2. Run a check

Every check needs `Authorization: Bearer <key>`. Without it you get `401`.

```sh
curl -s -X POST https://www.safegen.com.au/api/check \
  -H "authorization: Bearer $KEY" -H 'content-type: application/json' \
  -d '{"phone":"fixture:match"}'
```

Test keys accept only these practice values; a real phone number returns `400 test_fixtures_only`.

| Value | Response | What the platform should do |
|---|---|---|
| `fixture:match` | `listed: true, blockRequested: true, action: "reject"` | Refuse the account link |
| `fixture:no-block` | `listed: true, blockRequested: false, action: "allow"` | Carry on with your normal checks |
| `fixture:no-match` | `listed: false, blockRequested: false, action: "allow"` | Carry on with your normal checks |
| `fixture:unknown` | `listed: null, action: "unknown"` | Hold for retry or review |
| `fixture:error` | `503 simulated_outage` | Hold for retry or review |

A number not on the register is not proof the person is an adult; it only means no parent has registered it.

## 3. Move to real lookups (organisation sponsorship)

When a person at your organisation is ready to sponsor real lookups:

```sh
curl -s -X POST https://www.safegen.com.au/api/integrations/request-production \
  -H "authorization: Bearer $KEY" -H 'content-type: application/json' -d '{}'
```

Returns `202` with `status: "production_pending"`. SafeGen reviews the organisation and then issues a separate production key. Your test key keeps working on the practice values meanwhile. Human enquiries can also go through https://www.safegen.com.au/contact.

## Offline practice kit

```sh
git clone https://github.com/RicRicho/safegen-evaluation-kit.git
cd safegen-evaluation-kit
node --test test.mjs   # 12 tests
node example.mjs       # prints all five practice decisions
```

Runs only on your own machine with practice numbers, and makes no calls to SafeGen or any platform.

## Verified

20 Oct 2026 (Sydney), starting from the public pages only: signed up (201), duplicate sign-up refused (409), no-key check refused (401), all five practice values returned the results above, a real number on a test key was refused (400), and the production request was accepted for review (202).
