# One-test Codex web-search baseline

- Run: `av-zk0.3-dexter-codex-web-baseline/2026-06-10T04-04-57-866Z`
- Source eval repository: [`EntityProcess/financial-research-agent`](https://github.com/EntityProcess/financial-research-agent)
- Raw artifacts: [`index.jsonl`](index.jsonl), [`benchmark.json`](benchmark.json), [`timing.json`](timing.json), [`transcript.jsonl`](transcript.jsonl)

## What was evaluated

This was an early one-case live baseline for the native Dexter `llm-grader` rubric shape. It ran the TJX pre-tax-margin guidance beat/miss question through the AgentV `codex` provider target and graded the answer with the `dexter-rubric` LLM grader.

The larger 50-case run in [`age-14-task-bundle-dogfood/2026-06-10T08-35-26Z-age-14-codex`](../../age-14-task-bundle-dogfood/2026-06-10T08-35-26Z-age-14-codex/SUMMARY.md) is the better aggregate baseline. This one-test run is still useful because it demonstrates the public-web target, prompt-file resolution, Dexter rubric metadata rendering, and per-case artifact shape on a minimal live example.

## Score interpretation

Scores are on a 0.0-1.0 scale. The case score is the fraction of rubric checks satisfied. A full rubric pass requires every check to pass; this run completed but produced `execution_status: quality_failure` because the answer missed required criteria.

## Result

| Metric | Value |
| --- | ---: |
| Cases run | 1/1 |
| AgentV aggregate pass rate | 0.0% |
| Mean rubric score | 33.3% |
| Full rubric passes | 0/1 |
| Rubric checks satisfied | 1/3 (33.3%) |
| Total target tokens | 29,719 |
| Wall-clock duration | 35s |

| Case | Score | Checks | Interpretation |
| --- | ---: | ---: | --- |
| TJX Q4 FY2025 pre-tax-margin guidance beat/miss | 33.3% | 1/3 | The answer correctly stated the 70 bps beat versus the high end of guidance, but omitted the 80 bps beat versus the low end and therefore failed the full multi-part rubric. |

## What this baseline means

This run is a plumbing and artifact-shape proof, not a quality claim. It confirms that the financial eval pack can use AgentV's standard target execution, `llm-grader`, rubric assertions, transcript output, and raw JSONL artifacts without a bespoke Dexter-specific evaluator.

It is **not** a merge gate. Use the 50-case run for aggregate interpretation, and define explicit thresholds before treating future financial eval runs as release blockers.
