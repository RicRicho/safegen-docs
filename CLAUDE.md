# CLAUDE.md — SafeGen

## Project brief
SafeGen is a public documentation surface for Ric Richardson's privacy-preserving child-safety and age-assurance concept. The model: parents verify a child controls a mobile number; authorised platforms use a child-number registry to reduce under-age access — no face scans, no identity documents, minimal surveillance. Patent-backed at category level. This repo is documentation only, not an implementation repo.

## Goals
- Maintain clear, accurate public-facing documentation: problem framing, architecture-level notes, commercial context, and public review material.
- Consolidate and clean duplicate or experimental content.
- Support public positioning aligned with Australia's eSafety framework and comparable international regimes.

## Constraints
- Subscription auth only. Never write, add, or log an Anthropic or LLM API key.
- No credentials or secrets in any committed file. All secrets (SUPABASE_ACCESS_TOKEN, ANTHROPIC_API_KEY) are injected by the CI runner via GitHub secrets.
- This is a public-read repo — treat every commit as publicly visible.
- Do not add features or abstractions beyond what the task requires.

## Write-quarantine rules
Do NOT commit to this repository:
- Patent claim text, application numbers, or specification detail unless explicitly cleared for public release.
- HSM, registry, query, or platform-detection implementation detail.
- Named outreach targets, government briefings, investor/unitholder details, or commercial negotiations.
- Private data-room material from unrelated companies or projects.

## Warp event logging
For tasks dispatched from Warp, use the `warp-supabase` MCP server (configured in `.claude/settings.json`) to log progress and close the task row:

```sql
-- Log a step
SELECT cc_log_event('<task-id>', 'worker-step', '<what you did>');

-- Close the task
UPDATE tasks SET status = 'done', result = '<summary>' WHERE id = '<task-id>';
```

Log at least one `worker-step` per meaningful action and always close the task row (`done` or `failed`) before exiting.
