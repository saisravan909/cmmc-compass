# Contributing to CMMC Compass

Thank you for your interest in contributing to CMMC Compass. This document outlines the process for contributing code, documentation, and bug reports.

---

## Code of Conduct

All contributors are expected to be respectful, collaborative, and constructive. Harassment or exclusionary behavior of any kind is not tolerated.

---

## How to Contribute

### Reporting Bugs

Use the [Bug Report template](.github/ISSUE_TEMPLATE/bug_report.md). Include:
- A clear title and description
- Steps to reproduce
- Expected vs. actual behavior
- Browser, OS, and version information

### Requesting Features

Use the [Feature Request template](.github/ISSUE_TEMPLATE/feature_request.md). Include:
- The problem you are trying to solve
- Your proposed solution
- Which track it belongs to (Track 1 — Contractor, Track 3 — Consultancy)

### Submitting Pull Requests

1. Fork the repository and create a branch from `main`
2. Name your branch using the convention: `feat/<description>`, `fix/<description>`, or `docs/<description>`
3. Make your changes with clear, focused commits
4. Ensure all changes follow the existing code style
5. Open a pull request against `main` and fill out the PR template

---

## Commit Convention

All commits must follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>: <short description>

[optional body]
[optional footer]
```

**Types:**

| Type | When to use |
|---|---|
| `feat` | A new feature |
| `fix` | A bug fix |
| `docs` | Documentation changes only |
| `chore` | Build process, dependency updates, tooling |
| `refactor` | Code change that neither fixes a bug nor adds a feature |
| `test` | Adding or updating tests |

**Examples:**

```
feat: add live SPRS score calculation to dashboard
fix: correct evidence expiry date comparison logic
docs: update data model diagram in README
chore: seed all 110 CMMC Level 2 control definitions
```

---

## Branch Strategy

| Branch | Purpose |
|---|---|
| `main` | Stable, production-ready code |
| `feat/*` | Feature development |
| `fix/*` | Bug fixes |
| `docs/*` | Documentation updates |

All pull requests merge into `main` via squash merge.

---

## Development Setup

```bash
git clone https://github.com/saisravan909/cmmc-compass.git
cd cmmc-compass
pnpm install
cp .env.example .env
pnpm --filter @workspace/db run push
```

See [docs/architecture.md](docs/architecture.md) for full development environment documentation.

---

## Milestones & Labels

Work is organized into GitHub milestones by phase:

- `milestone: phase-1-mvp` — Core contractor compliance platform
- `milestone: phase-2-artifacts` — SSP/POA&M generation and export
- `milestone: phase-3-consultancy` — Multi-tenant MSP layer

Labels: `track-1`, `track-3`, `data-model`, `ux`, `export`, `auth`, `bug`, `enhancement`, `documentation`

---

## License

By contributing, you agree that your contributions will be licensed under the [MIT License](LICENSE).
