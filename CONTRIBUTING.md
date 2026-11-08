# Contributing to eve-agent

Bug reports, feature suggestions and pull requests are welcome. Please read the [Code of Conduct](CODE_OF_CONDUCT.md) first.

## Build and test

```bash
git clone https://github.com/Ankara-Software/eve-agent.git
cd eve-agent
bun install
bun run typecheck
bun run build
```

There is no automated test suite yet. `bun run typecheck` and `bun run build` are the checks. Node 24 is required (`engines.node` is `24.x`).

## Pull requests

1. Fork the repository and create a branch from the default branch.
2. Keep the change focused and make sure the commands above succeed.
3. Describe what changed and how you tested it in the pull request.

## Security

Do not report vulnerabilities in public issues. See [SECURITY.md](SECURITY.md).

## License

By contributing, you agree that your contributions are licensed under the repository license (see `LICENSE`).
