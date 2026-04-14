# Contributing

## Reporting Issues

Use the issue templates when filing a bug or feature request. For bugs, include steps to reproduce, expected behavior, and actual behavior. For features, describe the problem you are trying to solve and which track it belongs to.

## Opening a Pull Request

1. Fork the repo and create a branch from `main`
2. Name branches as `feat/description`, `fix/description`, or `docs/description`
3. Keep commits focused on one change at a time
4. Fill out the pull request template
5. All pull requests merge into `main` by squash merge

## Commit Format

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
feat: add SPRS score breakdown by domain
fix: evidence expiry date comparison off by one day
docs: update data model table for poam_items
chore: upgrade drizzle-orm to 0.30
```

Types: `feat`, `fix`, `docs`, `chore`, `refactor`, `test`

## Development Setup

```bash
git clone https://github.com/saisravan909/cmmc-compass.git
cd cmmc-compass
pnpm install
cp .env.example .env
pnpm --filter @workspace/db run push
```

## Labels and Milestones

Issues are tagged by track (`track-1`, `track-3`) and feature area (`evidence`, `scoring`, `ssp`, `poam`, etc.) and organized under three milestones matching the phases in the roadmap.

## License

By contributing you agree your work is licensed under the [MIT License](LICENSE).
