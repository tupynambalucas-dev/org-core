# tupynambalucas-dev Meta-Repository Agent Context

This document serves as the root context router (Layer 1) for AI agents operating in the
`tupynambalucas-dev/org-core` umbrella meta-repository.

## Workspace Navigation

- [README.md](./README.md): Primary developer documentation and submodule orchestration runbook.
- [tupynambalucas-dev.code-workspace](./tupynambalucas-dev.code-workspace): Canonical multi-root IDE workspace binding all four core submodules.
- [LICENSE](./LICENSE): Apache License 2.0 governing meta-repository orchestration assets.
- [.github](./.github/AGENTS.md): Organization governance, community health standards, and public profile.
- [agent-mesh](./agent-mesh/AGENTS.md): Enterprise AI agent mesh context router, MCP packages, domain plugins, and modular skills.
- [platform](./platform/AGENTS.md): Core platform monorepo containing services, apps, and Kubernetes manifests.
- [docs](./docs/AGENTS.md): Sovereign documentation hub built with Docusaurus v3 and Crowdin.

## Governance Standards

- **Branching Model**: Single-Branch GitHub Flow on `main`. Short-lived branches MUST use Conventional Commit prefixes (`feat/`, `fix/`, `docs/`, `chore/`, `refactor/`, `ci/`, `perf/`, `test/`, `build/`, `style/`, `revert/`, `hotfix/`).
- **Cryptographic Signature**: All Git commits and annotated tags MUST be signed with SSH (`git commit -S -m "..."`).
- **Conventional Commits**: All commit messages must follow `<type>[optional (<scope>)][!]: <description>` (`<= 72` chars target, `<= 100` chars maximum).
- **Zero-Emoji Policy**: Emojis are strictly forbidden across all code, PRs, comments, and agent interactions.
- **Secret Hygiene**: Never commit plaintext tokens. Environment variables cascade via Infisical or local/parent `.env` files.
- **License**: `Apache-2.0` (`Copyright (c) 2026 tupynambalucas.dev`) across all public repositories, packages, and plugins.

## Submodule Pointer Updates

Direct pushes to `main` are blocked by repository rulesets. After child repository Pull Requests are merged into their respective `main` branches, update submodule gitlink pointers in `org-core` via a signed Pull Request (or automated GitHub App GraphQL `createCommitOnBranch` dispatch):

```bash
git switch -c chore/bump-submodules
git add agent-mesh platform docs .github
git commit -S -m "chore(submodules): bump submodule pointers to latest main commits"
git push -u origin chore/bump-submodules
gh pr create --base main --title "chore(submodules): bump submodule pointers to latest main commits"
```

## Required Skills

Agents operating at the `org-core` meta-repository layer MUST autonomously engage the domain skills provided by [`agent-mesh`](./agent-mesh/plugins/README.md):

- **Atelier Plugin (`@tupynambalucas-dev/plugin-atelier`)**: `router-architect`, `skill-architect`, `rule-architect`, `hook-architect`, `plugin-architect`.
- **Repository Governance Plugin (`@tupynambalucas-dev/plugin-repo`)**: `readme-architect`, `monorepo-architect`, `community-health-architect`, `license-architect`.
- **GitHub Plugins (`@tupynambalucas-dev/plugin-github-org`, `@tupynambalucas-dev/plugin-github-flow`)**: `github-org-operator`, `github-ruleset-operator`, `github-security-auditor`, `github-app-operator`, `github-flow-operator`, `github-actions-operator`.
- **Secrets Plugin (`@tupynambalucas-dev/plugin-secrets`)**: `infisical-vault-operator`, `secret-rotation-operator`.
