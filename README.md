# tupynambalucas-dev Umbrella Meta-Repository

Central orchestrator and unified workspace for the `tupynambalucas-dev` organization.

This umbrella repository links autonomous corporate repositories via Git Submodules, providing unified cross-repository context, navigation, and developer orchestration while preserving independent Git histories, release cycles, and CI/CD pipelines.

---

## Ecosystem Architecture

```mermaid
graph TD
  direction TB

  Meta["org-core (Umbrella Meta-Repository)"]

  Meta --> Sub1[".github (Governance & Default Health)"]
  Meta --> Sub2["agent-mesh (Enterprise AI Agent Mesh)"]
  Meta --> Sub3["platform (Core Platform Monorepo)"]
  Meta --> Sub4["docs (Sovereign Documentation Hub)"]

  classDef repo fill:#1e1e2e,stroke:#89b4fa,stroke-width:2px,color:#cdd6f4;
  class Meta,Sub1,Sub2,Sub3,Sub4 repo;
```

### Managed Submodules

| Submodule | Target Branch | Purpose |
| :--- | :--- | :--- |
| [`.github`](./.github/README.md) | `main` | Organization-wide governance, community health files, public profile, and IDE templates. |
| [`agent-mesh`](./agent-mesh/README.md) | `main` | Universal AI agent governance monorepo, shared MCP connectors, domain plugins, and modular skills. |
| [`platform`](./platform/README.md) | `main` | Domain monorepo hosting Kubernetes manifests, Cortex AI gateway, studio tools, and services. |
| [`docs`](./docs/README.md) | `main` | Sovereign documentation portal built on Docusaurus v3 with Crowdin localization. |

### Multi-Root IDE Workspace

Open [tupynambalucas-dev.code-workspace](./tupynambalucas-dev.code-workspace) in VS Code or Antigravity IDE to mount all four submodules (`.github`, `platform`, `docs`, `agent-mesh`) in a unified multi-root workspace with integrated synchronization tasks.

---

## Environment Configuration and Secret Governance

The ecosystem implements a 3-tier fallback resolution architecture to ensure development environments operate smoothly whether launched with or without active Infisical sessions:

1. **Process Environment**: Variables already exported in the current shell session or injected via `infisical run`.
2. **Local and Ancestor `.env` Files**: If environment variables are absent from the shell, tools like `agent-mesh/scripts/mcp-gateway-router.js` walk up the directory tree to discover `.env` files located in the current workspace or at the `org-core` root.
3. **Infisical CLI**: If neither process variables nor local `.env` files satisfy the requirements, the system invokes `infisical export` using authenticated machine credentials or local login sessions.

### Execution Modes

#### A. Unified Meta-Repository (`org-core`)

When opening the entire `org-core` repository:

- You can maintain a root `.env` file (copied from `.env.example`) to provide shared credentials across all submodules.
- Alternatively, launch your commands or AI agent CLI through Infisical:

```bash
infisical run --projectId <PROJECT_ID> --env dev -- agy
```

#### B. Standalone Workspace Mode

When developing within an isolated submodule directory (`agent-mesh/`, `platform/`, or `docs/`):

- Each child repository contains its own `.env.example` template.
- Copy `.env.example` to `.env` inside the submodule root to test and execute tools without dependencies on parent repositories.
- Individual submodules can also be run directly with project-scoped Infisical commands:

```bash
# Inside agent-mesh:
infisical run --projectId <AGENT_MESH_PROJECT_ID> --env dev -- <command>

# Inside platform:
infisical run --projectId <PLATFORM_PROJECT_ID> --env dev -- <command>
```

---

## Getting Started

### 1. Clone with Submodules

To clone the umbrella repository and all nested submodules in a single pass:

```bash
git clone --recurse-submodules git@github.com:tupynambalucas-dev/org-core.git
cd org-core
```

### 2. Daily Synchronization

Fetch and merge the latest remote commits across all submodules:

```bash
git submodule update --remote --merge
```

To ensure submodules track their target branches rather than a detached HEAD:

```bash
git submodule foreach 'git checkout $(git config -f $toplevel/.gitmodules submodule.$name.branch || echo main)'
```

---

## Development Workflow and Governance

All development in this meta-repository and its submodules must comply with organizational governance:

1. **Cryptographic Signatures**: All Git commits and annotated tags MUST be signed using SSH (`git commit -S -m "..."`). Unsigned commits are rejected by repository rulesets.
2. **Conventional Commits**: Commit messages must follow the Conventional Commits v1.0.0 specification (`feat`, `fix`, `docs`, `chore`, etc.).
3. **Zero-Emoji Policy**: Emojis are strictly prohibited in commit messages, documentation, code comments, and chat responses.
4. **Submodule Pointer Updates**: Direct human pushes to `main` are blocked by repository rulesets. After merging child Pull Requests into each submodule's `main` branch, advance submodule pointers in `org-core` via a signed Pull Request (or automated GitHub App GraphQL dispatch):

```bash
git switch -c chore/bump-submodules
git add agent-mesh platform docs .github
git commit -S -m "chore(submodules): bump submodule pointers to latest main commits"
git push -u origin chore/bump-submodules
gh pr create --base main --title "chore(submodules): bump submodule pointers to latest main commits"
```

---

## License

Licensed under the [Apache License 2.0](./LICENSE). Copyright (c) 2026 tupynambalucas.dev.
