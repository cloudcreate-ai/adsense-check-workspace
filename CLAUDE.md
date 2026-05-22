# adsense-check-workspace

Monorepo for Google AdSense compliance checking tools.

## Projects

### adsense-check-core (core library)
- Package: `@cloudcreate/adsense-check-core`
- Shared business logic: crawling, checks, AI analysis, scoring, prompts
- Consumed by CLI, API, and future Web frontend
- Key commands: `npm run build -w adsense-check-core`, `npm run typecheck -w adsense-check-core`

### adsense-check-cli (CLI tool)
- Package: `@cloudcreate/adsense-check`
- Terminal interface wrapping core library
- Built with TypeScript, Commander.js, Playwright
- Key commands: `npm run dev -w adsense-check-cli`, `npm run build -w adsense-check-cli`

### adsense-check-api (Cloudflare Worker API)
- Package: `@cloudcreate/adsense-check-api`
- Hono-based API: AI proxy endpoints + full site check endpoints (planned)
- Deployed via Wrangler (Cloudflare Workers)
- Key commands: `npm run dev -w adsense-check-api`, `npm run deploy -w adsense-check-api`

### adsense-check-test (test suite)
- Package: `@cloudcreate/adsense-check-test`
- Vitest-based unit, integration, and e2e tests
- Tests core logic, CLI behavior, and API endpoints
- Key commands: `npm run test -w adsense-check-test`, `npm run typecheck -w adsense-check-test`

## Architecture

```
adsense-check-cli ─┐
                   ├→ adsense-check-core (depends on)
adsense-check-api ─┘
       ↑
adsense-check-test ──┘ (tests all modules)
```

All business logic lives in `core`. CLI and API are thin wrappers for their respective platforms.

## Quick Reference

| Task | Command |
|------|---------|
| Build all | `npm run build` |
| Typecheck all | `npm run typecheck` |
| Run CLI dev | `npm run dev -w adsense-check-cli` |
| Run API dev | `npm run dev -w adsense-check-api` |
| Run tests | `npm run test -w adsense-check-test` |
| Run API tests | `cd adsense-check-api && npx vitest run` |

## Agent Teams

Module ownership and coordination is defined in `.claude/agents.json`. The main Claude Code session acts as coordinator:

- **Single module change** → launch only the owning agent
- **Cross-module change** → launch all affected agents in parallel, coordinator reviews outputs
- **Core changes** → always coordinate with cli-team, api-team, and test-team (they all depend on core)
- **New feature** → core-team first, then cli-team + api-team in parallel, test-team last for coverage

### Team Quick Reference

| Team | Module | Owns |
|------|--------|------|
| core-team | adsense-check-core | Crawling, checks, AI analysis, scoring, shared types |
| cli-team | adsense-check-cli | CLI commands, output formatting, Playwright, npm publishing |
| api-team | adsense-check-api | Hono routes, AI proxy, Cloudflare Workers deployment |
| test-team | adsense-check-test | Unit, integration, e2e, cross-module compatibility tests |

## Backup

Original repositories are preserved in `backup/` during migration.
