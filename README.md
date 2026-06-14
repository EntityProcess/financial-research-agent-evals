# financial-research-agent-evals

Public-safe AgentV result artifacts for the `financial-research-agent` demo
project.

Source eval definitions live in `EntityProcess/financial-research-agent`. This repo
stores Dashboard-ready artifacts under `.agentv/results/runs/` only. Before
pushing artifacts, run the public artifact preflight from `agentv-deploy`:

```sh
python3 ../agentv-deploy/scripts/check-public-result-artifacts.py .
```

Writer credentials should come from `RESULT_SYNC_GITHUB_TOKEN` or local git/gh
auth and should be scoped only to this result repository where possible. Reader
mode is anonymous HTTPS clone/pull.

## Published validation runs

- [50-case Codex financial-research baseline](.agentv/results/runs/age-14-task-bundle-dogfood/2026-06-10T08-35-26Z-age-14-codex/SUMMARY.md) — aggregate public baseline over 50 Dexter-adapted financial research questions.
- [One-test Codex web-search baseline](.agentv/results/runs/av-zk0.3-dexter-codex-web-baseline/2026-06-10T04-04-57-866Z/SUMMARY.md) — early live plumbing check for the native Dexter `llm-grader` rubric shape.

The source/eval repository also has a public narrative report: [`EntityProcess/financial-research-agent` `BASELINE_RESULTS.md`](https://github.com/EntityProcess/financial-research-agent/blob/main/BASELINE_RESULTS.md).

## Static HTML reports

- [50-case Codex financial-research baseline report](docs/index.html) — generated with `agentv results report .agentv/results/runs/age-14-task-bundle-dogfood/2026-06-10T08-35-26Z-age-14-codex --out docs/index.html`.
- [One-case Dexter Codex web baseline report](docs/dexter-baseline.html) — generated with `agentv results report .agentv/results/runs/av-zk0.3-dexter-codex-web-baseline/2026-06-10T04-04-57-866Z --out docs/dexter-baseline.html`.

If GitHub Pages is enabled for this repository's `docs/` directory, `docs/index.html` can be served as the project homepage and `docs/dexter-baseline.html` as a secondary baseline page. Both files are self-contained, read-only AgentV reports and do not require a Dashboard server.
