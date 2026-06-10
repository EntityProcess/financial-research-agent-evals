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

- `.agentv/results/runs/av-zk0.3-dexter-codex-web-baseline/2026-06-10T04-04-57-866Z/` — one-test live Codex web-search baseline for the native Dexter `llm-grader` rubric shape.
