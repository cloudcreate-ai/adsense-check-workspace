# adsense-check-workspace

Monorepo for Google AdSense website compliance checking tools.

## Overview

`adsense-check` analyzes websites for Google AdSense review readiness. It detects "low value content" — the #1 rejection reason — using automated crawling, AI-powered content quality scoring, and stratified sampling. Supports content sites, tool sites, game sites, video sites, and reference sites.

## Packages

| Package | Description | npm |
|---------|-------------|-----|
| [`@cloudcreate/adsense-check`](./adsense-check-cli/) | CLI tool — install and run in your terminal | `npm i -g @cloudcreate/adsense-check` |
| [`@cloudcreate/adsense-check-core`](./adsense-check-core/) | Core library — crawling, checks, AI analysis, scoring | `npm i @cloudcreate/adsense-check-core` |
| [`@cloudcreate/adsense-check-api`](./adsense-check-api/) | Cloudflare Worker API — AI proxy + analysis endpoints | Deploy to Cloudflare Workers |
| `@cloudcreate/adsense-check-test` | Test suite — integration and e2e tests | (private) |

## Architecture

```
adsense-check-cli ─┐
                   ├→ @cloudcreate/adsense-check-core
adsense-check-api ─┘
       ↑
adsense-check-test ──┘ (tests all modules)
```

All business logic lives in `core`. CLI and API are thin wrappers for their respective platforms.

## Quick Start

### CLI (recommended for most users)

```bash
# Install globally
npm install -g @cloudcreate/adsense-check

# Check a website
adsense-check https://example.com

# Or run without installing
npx @cloudcreate/adsense-check https://example.com
```

### Development

```bash
# Clone with submodules
git clone --recursive git@github.com:cloudcreate-ai/adsense-check-workspace.git
cd adsense-check-workspace

# Install all dependencies
npm install

# Build all packages
npm run build

# Run CLI in dev mode
npm run dev -w adsense-check-cli

# Run API in dev mode
npm run dev -w adsense-check-api

# Run tests
npm run test -w adsense-check-test
```

## Submodules

This repository uses git submodules. Each module has its own repository, release cycle, and npm package:

- `adsense-check-core` → [cloudcreate-ai/adsense-check-core](https://github.com/cloudcreate-ai/adsense-check-core)
- `adsense-check-cli` → [cloudcreate-ai/adsense-checklist](https://github.com/cloudcreate-ai/adsense-checklist)
- `adsense-check-api` → [cloudcreate-ai/adsense-check-api](https://github.com/cloudcreate-ai/adsense-check-api)
- `adsense-check-test` → [cloudcreate-ai/adsense-check-test](https://github.com/cloudcreate-ai/adsense-check-test)

## License

MIT
