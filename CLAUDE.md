# CLAUDE.md — SafeGen

## Project brief
SafeGen is a public documentation surface for Ric Richardson's privacy-preserving child-safety and age-assurance concept. The model: parents verify a child controls a mobile number; authorised platforms use a child-number registry to reduce under-age access — no face scans, no identity documents, minimal surveillance. Patent-backed at category level. This repo is documentation only, not an implementation repo.

## Goals
- Maintain clear, accurate public-facing documentation: problem framing, architecture-level notes, commercial context, and public review material.
- Consolidate and clean duplicate or experimental content.
- Support public positioning aligned with Australia's eSafety framework and comparable international regimes.

## Constraints
- Subscription auth only. Never write, add, or log an Anthropic or LLM API key.
- No credentials or secrets in any committed file. All secrets (SUPABASE_ACCESS_TOKEN, ANTHROPIC_API_KEY, WARP_WRITE_KEY) are injected by the CI runner via GitHub secrets.
- This is a public-read repo — treat every commit as publicly visible.
- Do not add features or abstractions beyond what the task requires.

## Write-quarantine rules
Do NOT commit to this repository:
- Patent claim text, application numbers, or specification detail unless explicitly cleared for public release.
- HSM, registry, query, or platform-detection implementation detail.
- Named outreach targets, government briefings, investor/unitholder details, or commercial negotiations.
- Private data-room material from unrelated companies or projects.

## Report-back requirements (Warp-dispatched tasks)

The triggering issue body contains the task ID in this format:
```
Warp task: `TSK-YYYYMMDD-XXXX`
```

### (a) Branch and pull request — mandatory

Never commit code changes directly to `main`. For every Warp task:
1. Create a branch: `git checkout -b warp/<task-id>` (e.g. `warp/TSK-20260613-CWT4`)
2. Make all changes on that branch, commit, and push.
3. Open a pull request targeting `main` before exiting.

### (b) Write a cloud-build event on completion

Use the `WARP_WRITE_KEY` secret injected by CI — **not** `SUPABASE_ACCESS_TOKEN`:

```bash
TASK_ID="TSK-..."            # extracted from issue body
SUPABASE_URL="https://uswnbpyiepoaceretjjj.supabase.co"
SUMMARY="one-sentence description of what you did"

curl -s -X POST "$SUPABASE_URL/rest/v1/events" \
  -H "Authorization: Bearer $WARP_WRITE_KEY" \
  -H "apikey: $WARP_WRITE_KEY" \
  -H "Content-Type: application/json" \
  --data "$(jq -n --arg kind cloud-build --arg task_id "$TASK_ID" --arg body "$SUMMARY" \
    '{kind:$kind,task_id:$task_id,body:$body}')"
```

### (c) Close the task row

```bash
curl -s -X PATCH "$SUPABASE_URL/rest/v1/tasks?id=eq.$TASK_ID" \
  -H "Authorization: Bearer $WARP_WRITE_KEY" \
  -H "apikey: $WARP_WRITE_KEY" \
  -H "Content-Type: application/json" \
  --data "$(jq -n --arg status done --arg result "$SUMMARY" \
    '{status:$status,result:$result}')"
```

Use `"status":"failed"` and include the error in `result` if the task could not be completed.

### In-progress logging

Use the `warp-supabase` MCP (SUPABASE_ACCESS_TOKEN) for step logging during the task:
```sql
SELECT cc_log_event('<task-id>', 'worker-step', '<what you did>');
```
Log at least one `worker-step` per meaningful action.
