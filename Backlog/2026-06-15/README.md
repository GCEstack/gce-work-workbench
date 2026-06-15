# Backlog — 2026-06-15

## Status: Paused

Secrets and deployment audit completed. Backlog items added to the **Migration Phase 2** GitHub Project.

## Artifacts

- `C:\Users\Dekan AI Brother\api-inventory\secrets-inventory_20260615_0259.md`
- `C:\Users\Dekan AI Brother\api-inventory\secrets-inventory_20260615_0259.csv`

## What was audited

| Platform | Count |
|---|---|
| `01_ACTIVE` env files | 181 keys |
| Vercel projects | 11 |
| GitHub Actions secrets (all missing) | 8 repos |
| Fly.io apps | 4 |
| Supabase projects | 2 |
| Railway | TBD |
| Replicate | 1 token needed |

## Open backlog tasks (GitHub Project: Migration Phase 2)

1. Set GitHub Actions secrets for `gce-365-enpro-agent`
2. Set GitHub Actions secrets for `gce-365-vega-agent`
3. Set GitHub Actions secrets for `gce-ai-edge-crew-v3`
4. Set GitHub Actions secrets for `gce-ai-runway`
5. Set GitHub Actions secrets for `gce-work-epo-crowdsource`
6. Set GitHub Actions secrets for `gce-work-kimi-research`
7. Rename/relink Vercel projects from `simplebalance89-ais-projects` to `GCEstack`
8. Rename Fly.io apps to `gce-*` prefix and relink to GitHub
9. Map Supabase project refs to the correct GCE repos
10. Audit Railway projects and migrate env vars
11. Add `REPLICATE_API_TOKEN` to the repo(s) that use it
12. Re-enable `edge-crew-v3` GKE workflows (rename `workflows-disabled` → `workflows`)
13. `gce-ai-casa-companion` is last — do not migrate until explicitly requested

## Notes for next session

- The actual current source of truth is `C:\Users\Dekan AI Brother\Projects\01_ACTIVE`, not the copies in `dev\active` or `03_ARCHIVE`.
- `edge-crew-v3` currently has no GitHub secrets and its workflows folder is named `workflows-disabled`.
- Casa-companion Vercel projects stay on the old account for now.
