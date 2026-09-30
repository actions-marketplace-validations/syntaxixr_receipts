# Contributing

Thanks for looking. The quickest way in:

- **First contribution:** issues labeled [good first issue](https://github.com/syntaxixr/receipts/labels/good%20first%20issue) are small and say which files to touch.
- **Bigger work:** new runners are the main gap. [Go](https://github.com/syntaxixr/receipts/issues/2), [Rust](https://github.com/syntaxixr/receipts/issues/3) and [Java](https://github.com/syntaxixr/receipts/issues/4) each have an issue that explains how a runner plugs in.
- **A wrong verdict on your code** is the most useful bug report there is. Open an issue with the repository (or a minimal copy), the base branch, and what Receipts printed.

## Setup

```bash
npm ci
pip install pytest pytest-xdist
npm test
```

`npm test` builds and runs the suite against real pytest, vitest and jest projects in temporary git repositories.

## Rules that CI enforces

- The build in `plugin/skills/prove-fix/scripts/` is committed. Rebuild with `npm run build` and commit it with every change to `src/`.
- No runtime dependencies: `src/` uses Node built-ins only.
- Anything that touches the user's files goes through `src/swap.ts`, and every string from the repository under test goes through `src/sanitize.ts`. [SECURITY.md](SECURITY.md) explains why.
