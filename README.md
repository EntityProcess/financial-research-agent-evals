# financial-research-agent-evals

Public-safe AgentV result artifacts for the `financial-research-agent` demo
project.

Source eval definitions live in `christso/financial-research-agent`. This repo
stores Dashboard-ready artifacts under `.agentv/results/runs/` only. Before
pushing artifacts, run the public artifact preflight from `agentv-deploy`:

```sh
python3 ../agentv-deploy/scripts/check-public-result-artifacts.py .
```

Writer credentials should come from `RESULT_SYNC_GITHUB_TOKEN` or local git/gh
auth and should be scoped only to this result repository where possible. Reader
mode is anonymous HTTPS clone/pull.
