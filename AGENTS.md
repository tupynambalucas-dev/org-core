# tupynambalucas-dev Meta-Repository Agent Context

This document serves as the root context router (Layer 1) for AI agents operating in the
`tupynambalucas-dev/org-core` umbrella meta-repository.

## Workspace Navigation

- [README.md](./README.md): Primary developer documentation and submodule orchestration runbook.
- [.github](./.github/AGENTS.md): Organization governance, community health standards, and public profile.
- [agent-mesh](./agent-mesh/README.md): Enterprise AI agent governance plugin, shared MCP connectors, domain plugins, and modular skills.
- [platform](./platform/AGENTS.md): Core platform monorepo containing services, apps, and Kubernetes manifests.
- [docs](./docs/AGENTS.md): Sovereign documentation hub built with Docusaurus v3 and Crowdin.

## Governance Standards

- Cryptographic Signature: All Git commits and annotated tags MUST be signed with SSH (`git commit -S -m "..."`).
- Conventional Commits: All commit messages must follow `<type>(<scope>): <description>`.
- Zero-Emoji Policy: Emojis are strictly forbidden across all code, PRs, comments, and agent interactions.
- Secret Hygiene: Never commit plaintext tokens. Environment variables cascade via Infisical or local/parent `.env` files.

## Submodule Pointer Updates

When committing updates in child repositories, stage the updated submodule pointers in `org-core`:

```bash
git add agent-mesh platform docs .github
git commit -S -m "chore(submodules): bump pointers to latest development heads"
git push origin main
```

## Required Skills

- **`agent-router-expert`**: Active when creating or reviewing any `AGENTS.md` router file.
- **`markdown-expert`**: Active when creating, updating, or reviewing any `README.md` or general Markdown document.
- **`github-org-manager`**: Active when managing organization teams, permissions, or rulesets.
