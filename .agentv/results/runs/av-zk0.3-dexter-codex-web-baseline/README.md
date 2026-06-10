# av-zk0.3 Dexter Codex web baseline

One-test live baseline captured for the financial-research-agent Dexter eval rework.

- Source artifacts copied from `/tmp/financial-dexter-codex-baseline-live`.
- Financial PR commit: `0abdd598140503e18f699059d3c16eb950d81ea3` (`fix/dexter-agentv-prompt`).
- AgentV validation source: PR #1342 branch at `dcdde97d`.
- Command used `--target codex` from `.agentv/targets.yaml`; that target is the Codex web-research baseline target with the public-web system prompt and Azure grader target.
- Result is a quality failure for the captured TJX answer, but the run completed and verifies native `llm-grader` rubric plumbing, Dexter metadata, prompt-file resolution, and rendered rubric JSON in the grader request.
