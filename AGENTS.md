# tupynambalucas-dev Meta-Repository Agent Context

This document serves as the root context router (Layer 1) for AI agents operating in the
`tupynambalucas-dev/org-core` umbrella meta-repository.

## Workspace Navigation

- [README.md](./README.md): Primary developer documentation and Mani workspace orchestration runbook.
- [mani.yaml](./mani.yaml): Declarative multi-repository manifest managing repositories, remotes, and batch tasks.
- [tupynambalucas-dev.code-workspace](./tupynambalucas-dev.code-workspace): Canonical multi-root IDE workspace binding all five core repositories.
- [LICENSE](./LICENSE): Apache License 2.0 governing meta-repository orchestration assets.
- [.github](./.github/AGENTS.md): Organization governance, community health standards, and public profile.
- [.github-private](./.github-private/AGENTS.md): Organization internal governance, member-only profile, and enterprise AI settings.
- [agent-mesh](./agent-mesh/AGENTS.md): Enterprise AI agent mesh context router, MCP packages, domain plugins, and modular skills.
- [platform](./platform/AGENTS.md): Core platform monorepo containing services, apps, and Kubernetes manifests.
- [docs](./docs/AGENTS.md): Sovereign documentation hub built with Docusaurus v3 and Crowdin.
- [workstation](./workstation/AGENTS.md): Sovereign developer workstation engineering, WSL2 custom distributions, and CLI suite.

## Governance Standards

- **Branching Model**: Single-Branch GitHub Flow on `main`. Short-lived branches MUST use Conventional Commit prefixes (`feat/`, `fix/`, `docs/`, `chore/`, `refactor/`, `ci/`, `perf/`, `test/`, `build/`, `style/`, `revert/`, `hotfix/`).
- **Cryptographic Signature**: All Git commits and annotated tags MUST be signed with SSH (`git commit -S -m "..."`).
- **Conventional Commits**: All commit messages must follow `<type>[optional (<scope>)][!]: <description>` (`<= 72` chars target, `<= 100` chars maximum).
- **Zero-Emoji Policy**: Emojis are strictly forbidden across all code, PRs, comments, and agent interactions.
- **Secret Hygiene**: Never commit plaintext tokens. Environment variables cascade via Infisical or local/parent `.env` files.
- **License**: `Apache-2.0` (`Copyright (c) 2026 tupynambalucas.dev`) across all public repositories, packages, and plugins.
- **Workspace Orchestration**: Repositories are managed as sovereign Git repositories coordinated via `mani`. Git submodules and `160000` commit gitlinks are deprecated and removed.

## Multi-Repository Operations with Mani

Cross-repository commands and queries are executed using `mani`:

```bash
# Check status across all managed repositories
mani run status

# Fetch remote changes for all repositories
mani run fetch

# Pull latest main across all repositories
mani run pull

# Display current branches
mani run branch
```

## AI Agent Plugin Consumption (Dual Consumption Model)

The organization operates under a unified Dual Consumption Model for AI agent plugins and skills:

1. **Meta-Repository Mode (`org-core`)**:
   - The root [`.agents/plugins.json`](./.agents/plugins.json) registers local relative paths directly:
     ```json
     {
       "entries": [
         { "path": "agent-mesh/plugins/packages" },
         { "path": "platform/.agents/plugins" }
       ]
     }
     ```
   - This enables real-time hot-reloading of agent plugins and MCP servers across the entire multi-root IDE workspace without intermediate package building or installation steps.
2. **External & Standalone Monorepo Mode (`omnichannel`, `platform`, `docs`)**:
   - External services and isolated child repositories consume the unified umbrella package `@tupynambalucas-dev/agent-mesh` via `catalogs.plugins-stack` in `pnpm-workspace.yaml`:
     ```yaml
     catalogs:
       plugins-stack:
         '@tupynambalucas-dev/agent-mesh': 'github:tupynambalucas-dev/agent-mesh'
     ```
   - Consumer `.agents/plugins.json` files declare:
     ```json
     {
       "entries": [
         { "path": "node_modules/@tupynambalucas-dev/agent-mesh/plugins/packages" }
       ]
     }
     ```
   - All 10 domain plugins (`appsheet`, `atelier`, `docusaurus`, `github-flow`, `github-org`, `gwork`, `repo`, `research`, `secrets`, `web`) and 8 sovereign MCP servers execute seamlessly via self-contained launchers (`scripts/launcher.cjs`) and committed bundles (`dist/bin.cjs`).

## Architectural Plans & Artifact Dual-Storage Standard

Architectural blueprints, technical plans, and master plans follow strict enterprise storage standards:
- **Storage Location**: Blueprints reside in `<repo>/.agents/plans/<plan-slug>/`.
- **Topologies**: Topology 1 (Single-File Plan) for atomic refactors/features; Topology 2 (Multi-Artifact Plan Suite) for multi-domain frameworks with master `README.md` and numbered domain documents.
- **Dual-Storage Invariant**: Whenever an agent creates a plan artifact in the Antigravity conversation directory (`<appDataDir>/brain/<conversation-id>/`), an identical synchronized copy MUST ALWAYS be mirrored in `<repo>/.agents/plans/<plan-slug>/`.
- **Ignore & Index Triad**: All repositories ignore `.agents/plans/` and `plans/` in `.gitignore`, while explicitly un-ignoring them in `.ignore` and `.rgignore` (`!.agents/plans/`, `!.agents/plans/**`, `!plans/`, `!plans/**`) and setting `"search.useIgnoreFiles": false` in `.vscode/settings.json` so files can always be attached with `@`.

## Required Skills

Agents operating at the `org-core` meta-repository layer MUST autonomously engage the domain skills provided by [`agent-mesh`](./agent-mesh/plugins/README.md):

- **Atelier Plugin (`@tupynambalucas-dev/plugin-atelier`)**: `router-architect`, `skill-architect`, `rule-architect`, `hook-architect`, `plugin-architect`, `plan-architect`.
- **Repository Governance Plugin (`@tupynambalucas-dev/plugin-repo`)**: `readme-architect`, `monorepo-architect`, `community-health-architect`, `license-architect`, `github-standards-architect`, `mani-operator`.
- **GitHub Plugins (`@tupynambalucas-dev/plugin-github-org`, `@tupynambalucas-dev/plugin-github-flow`)**: `github-org-operator`, `github-ruleset-operator`, `github-security-auditor`, `github-app-operator`, `github-flow-operator`, `github-actions-operator`.
- **Secrets Plugin (`@tupynambalucas-dev/plugin-secrets`)**: `infisical-vault-operator`, `secret-rotation-operator`.
