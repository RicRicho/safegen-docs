# SafeGen visiting-agent discovery

**Updated:** 20 October 2026 (Australia/Sydney)
**Owner:** Sam, SafeGen manager (Linear RIC-226 / RIC-78)
**Purpose:** a plain public guide so an agent that has never seen SafeGen can find the service, try it with test data, and explain the result to its human, with no private help.

## What SafeGen offers platforms

SafeGen keeps a register of phone numbers that parents have put on the Safe List because they belong to a child. A platform calls SafeGen at sign-up, before it creates an account, and asks whether the phone number is on the register and whether the parent asked for it to be blocked.

- Live site: https://www.safegen.com.au/
- Platform guide (human-readable): https://www.safegen.com.au/api-docs
- Developer sign-up (self-serve test key): https://www.safegen.com.au/developers/sign-up

## Step 1: get a test key (self-serve)

Fill in the form at https://www.safegen.com.au/developers/sign-up, or call it directly:

```sh
curl -X POST https://www.safegen.com.au/api/integrations/signup \
  -H "Content-Type: application/json" \
  -d '{"orgName":"Your organisation","contactName":"Your name","contactEmail":"you@example.com","website":"https://example.com"}'
```

`orgName` is required. The reply contains a test key starting `sg_test_`. Keep it secret.

## Step 2: run a check with test data

Every check needs the key. A call without one is refused with `401` and a message pointing to the sign-up page.

```sh
curl -X POST https://www.safegen.com.au/api/check \
  -H "Authorization: Bearer sg_test_YOUR_KEY" \
  -H "Content-Type: application/json" \
  -d '{"countryCode":"+61","phone":"fixture:match"}'
```

Test keys accept only practice values (`fixture:match`, `fixture:no-match`, `fixture:no-block`, `fixture:unknown`, `fixture:error`) and are rate limited per hour. They never look up real numbers.

Reply fields:

| Field | Meaning |
|---|---|
| `listed` | the number is on the register (`null` when the answer is inconclusive) |
| `blockRequested` | the parent asked platforms to block this number |
| `action` | `reject` when listed with a block request; `allow` otherwise; `unknown` when inconclusive |
| `checkedAt` | time of the check |

How to explain the result: `reject` means do not create the account; `allow` means carry on with your other checks (a number not on the list is not proof the person is an adult); `unknown` or an error means hold the sign-up for retry or review.

## Step 3: move to production

With a test key, request production access:

```
POST https://www.safegen.com.au/api/integrations/request-production
Authorization: Bearer sg_test_YOUR_KEY
```

SafeGen reviews the organisation and then issues a production key, which performs real register lookups.

## Offline practice kit (no key, no network)

For a fully offline trial there is a free, MIT-licensed practice kit:

- Repo: https://github.com/RicRicho/safegen-evaluation-kit (release v0.1.0)

```sh
git clone https://github.com/RicRicho/safegen-evaluation-kit.git
cd safegen-evaluation-kit
node --test test.mjs   # 12 tests
node example.mjs       # prints the five practice outcomes and the right decision for each
```

It runs only on your own machine (127.0.0.1), uses practice numbers only, allows 30 requests and 1 KiB bodies.

## Other public pages

- Scoreboard: https://www.safegen.com.au/scoreboard
- Public counters (JSON): https://www.safegen.com.au/api/stats
- Concept docs: https://ricricho.github.io/safegen-docs/
- Press kit: https://safegen.gitbook.io/press-kit/

## Checked 20 October 2026 (Sydney)

From a clean machine with no SafeGen or GitHub login: the live site, platform guide and developer sign-up page all load; `POST /api/check` without a key returns `401` with sign-up guidance; the sign-up route answers (an empty request returns `org_name_required`); the production request route requires a key; and the offline kit passes 12 of 12 tests and prints all five outcomes.

Still to do: a published machine-readable description (OpenAPI) and `llms.txt` on www.safegen.com.au itself.
