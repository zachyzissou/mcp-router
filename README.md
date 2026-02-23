# mcp-router

> A cross-platform desktop app for managing MCP servers with local-first configuration and observability-friendly operations.
> Status: `maintenance`

![CI](https://img.shields.io/github/actions/workflow/status/zachyzissou/mcp-router/.github/workflows/baseline-ts-ci.yml)
![License](https://img.shields.io/github/license/zachyzissou/mcp-router)
![Security](https://img.shields.io/badge/security-SECURITY.md-green)

## Overview
MCP Router helps users add, configure, and monitor local or remote MCP servers in one place.
This repository contains the app shell, shared packages, and electron runtime integration used to interact with desktop MCP workflows.

## Problem / Value
- **Problem:** MCP server configuration can become fragmented across clients and manual scripts.
- **Value:** Consolidates configuration, import/export, and operational visibility in a single workspace.
- **Users:** Desktop users managing MCP-based integrations for AI tooling.

```text
UI Dashboard --> MCP Registry --> Worker Orchestrator --> Local Stores
                         \--> Telemetry/Logs --> Health checks
```

## Features
- ✅ Cross-platform desktop package setup and shared server abstractions.
- ✅ Universal MCP server add/connect workflows.
- ✅ Import/export and persistence of configuration data.
- ⏳ Add hardening checklist for release pipeline and runtime hardening.

## Tech Stack
- Runtime: Node.js `>=20` (CI uses `22`) with Electron
- Framework: TypeScript, Turborepo
- Tooling: pnpm, Turborepo, ESLint, TypeScript
- CI: GitHub Actions
- Storage: Local filesystem / local DB (app-scoped)

## Prerequisites
- Node.js >= 20 and pnpm >= 8
- Git
- Platform-specific Electron build tooling when producing installers

## Installation
```bash
# clone repo
git clone https://github.com/zachyzissou/mcp-router.git
cd mcp-router

# install dependencies
pnpm install

# run dev workspace
pnpm dev
```

## Configuration
| Key | Required | Default | Notes |
| --- | --- | --- | --- |
| `NODE_ENV` | no | `development` | Local environment mode |
| `APP_DATA_DIR` | no | app default | Override local app data directory |
| `LOG_LEVEL` | no | `info` | Logger level for local diagnostics |

## Usage
```bash
pnpm dev
```

```bash
# optional production build
pnpm build
```

## Testing & Quality
```bash
pnpm run lint
pnpm run typecheck
pnpm run build
pnpm run test:e2e
```

- Current baseline gates now include lint/typecheck/build/test-if-present checks with script-presence guards.
- Suggested quality target: maintain clean lint/typecheck signal on touched areas and keep workspace builds reproducible.

## Security
- Report issues via `SECURITY.md`.
- Never commit credentials or tokens.
- Prefer secure storage for all local secret material.
- Add Dependabot/CodeQL where feasible and keep branch protection enabled.

## Contributing
1. Create a branch from `main`.
2. Document assumptions and local verification steps in PR.
3. Run baseline checks and include outputs.
4. Seek review on CI and risk summary before merge.

## Deployment / runbook
- Deployment target: tagged release artifacts (installer workflows are externalized to existing app release path).
- Rollback: revert release commit/tag and re-run pinned workspace installer build.
- Emergency action: disable publish jobs, revert risky config changes, and reopen issue.

## Troubleshooting
- Symptom: App fails to install dependencies
  - Check Node/pnpm versions and run `pnpm install --frozen-lockfile`.
- Symptom: Typecheck errors in monorepo
  - Run `pnpm run typecheck` for local scope and inspect package-level cache artifacts.

## Observability
- Health target: app startup success and worker bootstrap logs.
- Logs: local runtime logs and CI logs in GitHub Actions.
- Alerts: repository issue tracker and maintainer inbox.
- SLO: stable startup and clean typecheck/build on mainline changes.

## Roadmap
- Q1: Baseline governance and security policy alignment.
- Q2: Add reproducible packaging checks and release docs.
- Q3: Add explicit observability and rollback runbook in release playbook.

## Known Risks
- Electron runtime dependency volatility.
- Build output size may increase with workspace growth.
- Branch divergence from upstream forks/repositories of MCP tooling.

## Release Notes
- `1.0.0`: baseline README + governance files and baseline CI workflow.

## Changelog
See `CHANGELOG.md` if present in the future.

## License
See [LICENSE.md](LICENSE.md)

## Contact
- Maintainer: `security@example.com`
- Security contact: see [SECURITY.md](SECURITY.md)
