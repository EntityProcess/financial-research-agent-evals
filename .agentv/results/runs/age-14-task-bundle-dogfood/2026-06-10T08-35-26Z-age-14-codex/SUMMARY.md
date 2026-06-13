# Financial research Codex baseline results

- Run: `age-14-task-bundle-dogfood/2026-06-10T08-35-26Z-age-14-codex`
- Source eval repository: [`EntityProcess/financial-research-agent`](https://github.com/EntityProcess/financial-research-agent)
- Source eval file: [`evals/financial-research-agent.eval.yaml`](https://github.com/EntityProcess/financial-research-agent/blob/main/evals/financial-research-agent.eval.yaml)
- Raw artifacts: [`index.jsonl`](index.jsonl), [`benchmark.json`](benchmark.json), [`timing.json`](timing.json), [`transcript.jsonl`](transcript.jsonl)

## What was evaluated

This run evaluates a public financial-research target agent on 50 questions adapted from Dexter's public `finance_agent.csv` fixture at commit `8d9419829f443f84b804d033bb2c3b1fbd788629`. The questions cover retrieval, numerical reasoning, beat/miss calculations, trend analysis, market analysis, adjustments, and financial modeling.

- **Target/harness:** AgentV `codex` provider target named `codex`, using the public web-research prompt in the source repo's `.agentv/targets.yaml`.
- **Model:** the Codex model is supplied through the source repo's `CODEX_MODEL` environment variable; the public artifact records the target label but does not export the exact model name.
- **Grader:** AgentV `llm-grader` named `dexter-rubric`, using Dexter rubric metadata preserved as structured AgentV rubric items. The public artifact records an Azure/OpenAI-compatible grader target label, but no endpoint or key.
- **No Dexter runtime dependency:** Dexter is fixture provenance and golden-answer/rubric source. The target was instructed not to use Dexter, private datasets, paid market-data services, or benchmark answers as answer sources.

## Score interpretation

Scores are on a 0.0-1.0 scale. Each case has rubric assertions; the case score is the fraction of checks satisfied. A full rubric **pass** means every check passed. `execution_status: quality_failure` means the run completed but the answer did not meet the configured quality threshold; it is not an infrastructure crash.

## Headline result

| Metric | Value |
| --- | ---: |
| Cases run | 50/50 |
| AgentV aggregate pass rate | 72.0% |
| Mean rubric score | 81.3% |
| Median rubric score | 100.0% |
| Full rubric passes | 32/50 |
| `execution_status: ok` | 36/50 |
| Rubric checks satisfied | 192/241 (79.7%) |
| Total target tokens | 2,852,820 |
| Wall-clock duration | 1h 8m 5s |

The baseline is strongest on direct quantitative retrieval, qualitative retrieval, and many formulaic numerical-reasoning tasks. It is weaker on market-analysis questions and exact multi-part answers where a single omitted date, low-end range, or stale benchmark fact can fail several checks.

## Breakdown by question type

| Question type | Cases | Mean score | AgentV ok | Full rubric passes |
| --- | ---: | ---: | ---: | ---: |
| Adjustments | 4 | 75.0% | 3/4 | 3/4 |
| Beat or Miss | 7 | 79.2% | 5/7 | 4/7 |
| Complex Retrieval | 3 | 87.8% | 3/3 | 1/3 |
| Financial Modeling | 4 | 88.6% | 3/4 | 3/4 |
| Market Analysis | 3 | 32.9% | 0/3 | 0/3 |
| Numerical Reasoning | 8 | 84.4% | 6/8 | 6/8 |
| Qualitative Retrieval | 9 | 91.4% | 7/9 | 7/9 |
| Quantitative Retrieval | 9 | 82.2% | 7/9 | 7/9 |
| Trends | 3 | 85.6% | 2/3 | 1/3 |

## Representative cases

| Row | Score | Checks | Case | What it shows |
| ---: | ---: | ---: | --- | --- |
| 29 | 100.0% | 17/17 | List the Operating KPIs Spirit Airlines (NYSE: SAVE) tracked in FY 2024… | Broad KPI enumeration passed all 17 checks. |
| 36 | 100.0% | 4/4 | What price was RDFN acquired at? (include price per share, equity value… | Acquisition terms matched price per share, equity value, and enterprise value. |
| 37 | 100.0% | 2/2 | As of Dec 31, 2024, what was Warner Bros. Discovery's (NASDAQ: WBD) Tot… | Simple quantitative retrieval matched the published restructuring-cost figure. |
| 43 | 100.0% | 10/10 | What portion of Uber’s 2024 revenue growth was driven by take-rate expa… | Multi-step revenue-growth attribution passed all 10 checks. |
| 1 | 20.0% | 1/5 | How has US Steel addressed its planned merger with Nippon Steel and its… | Pinned reference expected a blocked U.S. Steel/Nippon deal, while the target answered with later public-web developments; this is a benchmark-drift warning as much as a target-quality signal. |
| 3 | 66.7% | 2/3 | Did TJX beat or miss its Q4 FY 2025 pre-tax margin guidance? Express re… | One part of a two-sided beat/miss answer was omitted: high-end guidance was correct, low-end guidance was missing. |
| 46 | 28.6% | 2/7 | As of December 2024, what has been Zillow's (NASDAQ:Z) acquisition stra… | Date-specific acquisition-strategy criteria were only partially satisfied. |
| 50 | 0.0% | 0/6 | By how much did AMD beat/miss its non-GAAP gross profit guide (implied… | AMD guidance/gross-profit calculation missed all rubric checks in this run. |

## Full per-case table

| Row | Question type | Score | Checks | Verdict | Case | Question |
| ---: | --- | ---: | ---: | --- | --- | --- |
| 1 | Market Analysis | 20.0% | 1/5 | fail | [how-has-us-steel-addressed-its-planned-merger-with-nippon-steel-and-its-](financial-research-agent/how-has-us-steel-addressed-its-planned-merger-with-nippon-steel-and-its-/) | How has US Steel addressed its planned merger with Nippon Steel and its effect on its business operations? |
| 2 | Trends | 90.0% | 9/10 | fail | [how-has-netflix-s-nasdaq-nflx-average-revenue-per-paying-user-changed-fr](financial-research-agent/how-has-netflix-s-nasdaq-nflx-average-revenue-per-paying-user-changed-fr/) | How has Netflix's (NASDAQ: NFLX) Average Revenue Per Paying User Changed from 2019 to 2024? |
| 3 | Beat or Miss | 66.7% | 2/3 | fail | [did-tjx-beat-or-miss-its-q4-fy-2025-pre-tax-margin-guidance-express-resu](financial-research-agent/did-tjx-beat-or-miss-its-q4-fy-2025-pre-tax-margin-guidance-express-resu/) | Did TJX beat or miss its Q4 FY 2025 pre-tax margin guidance? Express result as BPS difference |
| 4 | Complex Retrieval | 80.0% | 4/5 | fail | [how-large-was-the-range-in-terms-for-amd-s-revenue-guidance-for-q2-2024-](financial-research-agent/how-large-was-the-range-in-terms-for-amd-s-revenue-guidance-for-q2-2024-/) | How large was the range (in % terms) for AMD's revenue guidance for Q2 2024, Q3 2024, Q4 2024, and Q1 2025? F… |
| 5 | Qualitative Retrieval | 100.0% | 9/9 | pass | [in-2024-who-was-nominated-to-serve-on-bbsi-s-nasdaq-bbsi-board-of-direct](financial-research-agent/in-2024-who-was-nominated-to-serve-on-bbsi-s-nasdaq-bbsi-board-of-direct/) | In 2024, who was Nominated to Serve on BBSI's (NASDAQ: BBSI) Board of Directors? |
| 6 | Complex Retrieval | 100.0% | 5/5 | pass | [of-amzn-meta-or-goog-who-plans-to-spend-the-most-in-capex-in-2025](financial-research-agent/of-amzn-meta-or-goog-who-plans-to-spend-the-most-in-capex-in-2025/) | Of AMZN, META, or GOOG, who plans to spend the most in capex in 2025? |
| 7 | Qualitative Retrieval | 100.0% | 2/2 | pass | [who-is-the-current-cfo-of-airbnb-nasdaq-abnb](financial-research-agent/who-is-the-current-cfo-of-airbnb-nasdaq-abnb/) | Who is the current CFO of Airbnb (NASDAQ: ABNB)? |
| 8 | Quantitative Retrieval | 0.0% | 0/2 | fail | [what-was-the-total-consideration-cost-tko-paid-to-acquired-endeavor-asse](financial-research-agent/what-was-the-total-consideration-cost-tko-paid-to-acquired-endeavor-asse/) | What was the total consideration cost TKO paid to acquired Endeavor assets measured at transaction close? |
| 9 | Beat or Miss | 100.0% | 2/2 | pass | [how-many-basis-points-did-mu-beat-or-miss-its-q3-2024-gaap-gross-margin-](financial-research-agent/how-many-basis-points-did-mu-beat-or-miss-its-q3-2024-gaap-gross-margin-/) | How many basis points did MU beat or miss its Q3 2024 GAAP gross margin guidance? |
| 10 | Numerical Reasoning | 100.0% | 4/4 | pass | [calculate-the-3-year-revenue-cagr-for-palantir-technologies-from-2021-to](financial-research-agent/calculate-the-3-year-revenue-cagr-for-palantir-technologies-from-2021-to/) | Calculate the 3 year revenue CAGR for Palantir Technologies from 2021 to 2024. |
| 11 | Quantitative Retrieval | 40.0% | 2/5 | fail | [how-many-common-stock-shares-are-outstanding-for-abnb-format-class-x-x-s](financial-research-agent/how-many-common-stock-shares-are-outstanding-for-abnb-format-class-x-x-s/) | How many common stock shares are outstanding for ABNB? Format "Class X: X shares" add line break. |
| 12 | Financial Modeling | 54.5% | 6/11 | fail | [february-financials-for-tsm-have-been-released-as-of-march-10-2025-assum](financial-research-agent/february-financials-for-tsm-have-been-released-as-of-march-10-2025-assum/) | February financials for TSM have been released as of March 10, 2025. Assuming revenue in March 2025 grows at… |
| 13 | Numerical Reasoning | 100.0% | 2/2 | pass | [what-is-the-total-amount-of-director-compensation-in-dollars-that-was-pa](financial-research-agent/what-is-the-total-amount-of-director-compensation-in-dollars-that-was-pa/) | What is the total amount of director compensation (in dollars) that was paid to the directors of 3D Systems i… |
| 14 | Trends | 66.7% | 4/6 | fail | [approximate-zillow-s-free-cash-flow-as-cfo-capex-what-is-the-trend-of-fc](financial-research-agent/approximate-zillow-s-free-cash-flow-as-cfo-capex-what-is-the-trend-of-fc/) | Approximate Zillow's Free Cash Flow as CFO - Capex. What is the trend of FCF margin over the last 3 years? |
| 15 | Numerical Reasoning | 100.0% | 4/4 | pass | [calculate-the-inventory-turnover-for-us-steel-in-fy2024](financial-research-agent/calculate-the-inventory-turnover-for-us-steel-in-fy2024/) | Calculate the inventory turnover for US Steel in FY2024. |
| 16 | Complex Retrieval | 83.3% | 10/12 | fail | [summarize-the-key-terms-of-the-series-d-mandatory-convertible-preferred-](financial-research-agent/summarize-the-key-terms-of-the-series-d-mandatory-convertible-preferred-/) | Summarize the key terms of the Series D mandatory convertible preferred stock (size of offering, closing date… |
| 17 | Trends | 100.0% | 5/5 | pass | [how-has-airbnb-s-annual-take-rate-revenue-gross-booking-value-trended-fr](financial-research-agent/how-has-airbnb-s-annual-take-rate-revenue-gross-booking-value-trended-fr/) | How has Airbnb's Annual Take Rate (Revenue/Gross Booking Value) Trended from FY 2022 - 2024? List the take ra… |
| 18 | Qualitative Retrieval | 100.0% | 6/6 | pass | [does-workday-nasdaq-wday-report-a-gross-or-net-retention-metric-in-its-a](financial-research-agent/does-workday-nasdaq-wday-report-a-gross-or-net-retention-metric-in-its-a/) | Does Workday (NASDAQ: WDAY) report a gross or net retention metric in its annual or quarterly reporting? If s… |
| 19 | Numerical Reasoning | 100.0% | 2/2 | pass | [what-is-the-total-value-of-msci-s-operating-leases-in-s-thousands-that-a](financial-research-agent/what-is-the-total-value-of-msci-s-operating-leases-in-s-thousands-that-a/) | What is the total value of MSCI's operating leases (in $'s, thousands) that are maturing in the next three ye… |
| 20 | Numerical Reasoning | 75.0% | 3/4 | fail | [what-was-orcl-s-effective-tax-rate-for-the-fiscal-year-ended-5-31-2024-a](financial-research-agent/what-was-orcl-s-effective-tax-rate-for-the-fiscal-year-ended-5-31-2024-a/) | What was ORCL's effective tax rate for the fiscal year ended 5/31/2024 and how did it change vs. the prior ye… |
| 21 | Qualitative Retrieval | 66.7% | 2/3 | fail | [what-is-shift4-s-vendor-concentration-risk-as-of-dec-31-2024](financial-research-agent/what-is-shift4-s-vendor-concentration-risk-as-of-dec-31-2024/) | What is Shift4's vendor concentration risk as of Dec 31, 2024? |
| 22 | Numerical Reasoning | 0.0% | 0/4 | fail | [what-was-abnb-s-gross-booking-per-room-night-gross-booking-value-divided](financial-research-agent/what-was-abnb-s-gross-booking-per-room-night-gross-booking-value-divided/) | What was ABNB's gross booking per room night (gross booking value divided by number of nights and experiences… |
| 23 | Qualitative Retrieval | 100.0% | 2/2 | pass | [when-is-production-expected-to-begin-in-j-m-smucker-s-nyse-sjm-new-distr](financial-research-agent/when-is-production-expected-to-begin-in-j-m-smucker-s-nyse-sjm-new-distr/) | When is production expected to begin in J M Smucker's (NYSE: SJM) new distribution center in McCalla, Alabama? |
| 24 | Numerical Reasoning | 100.0% | 2/2 | pass | [as-of-march-10-2025-what-is-the-face-value-of-salesforce-s-debt-excludin](financial-research-agent/as-of-march-10-2025-what-is-the-face-value-of-salesforce-s-debt-excludin/) | As of March 10, 2025, what is the face value of Salesforce's debt excluding their sustainability notes? |
| 25 | Qualitative Retrieval | 55.6% | 5/9 | fail | [summarize-the-regulatory-risks-paylocity-s-nasdaq-pcty-lists-in-its-fy-2](financial-research-agent/summarize-the-regulatory-risks-paylocity-s-nasdaq-pcty-lists-in-its-fy-2/) | Summarize the regulatory risks Paylocity's (NASDAQ: PCTY) lists in its FY 2024 10-K. |
| 26 | Numerical Reasoning | 100.0% | 2/2 | pass | [as-of-june-30-2024-what-of-microsoft-s-nasdaq-msft-full-time-employees-a](financial-research-agent/as-of-june-30-2024-what-of-microsoft-s-nasdaq-msft-full-time-employees-a/) | As of June 30, 2024, what % of Microsoft's (NASDAQ: MSFT) full-time employees are located outside of the Unit… |
| 27 | Qualitative Retrieval | 100.0% | 6/6 | pass | [as-of-fy-2024-what-are-the-terms-of-the-junior-subordinated-debentures-i](financial-research-agent/as-of-fy-2024-what-are-the-terms-of-the-junior-subordinated-debentures-i/) | As of FY 2024, what are the terms of the Junior Subordinated Debentures in the Allstate Corporation's (NYSE:… |
| 28 | Quantitative Retrieval | 100.0% | 2/2 | pass | [what-are-netflix-s-nasdaq-nflx-total-projected-material-cash-requirement](financial-research-agent/what-are-netflix-s-nasdaq-nflx-total-projected-material-cash-requirement/) | What are Netflix's (NASDAQ: NFLX) Total Projected Material Cash Requirements for 2025? |
| 29 | Qualitative Retrieval | 100.0% | 17/17 | pass | [list-the-operating-kpis-spirit-airlines-nyse-save-tracked-in-fy-2024-pro](financial-research-agent/list-the-operating-kpis-spirit-airlines-nyse-save-tracked-in-fy-2024-pro/) | List the Operating KPIs Spirit Airlines (NYSE: SAVE) tracked in FY 2024. Provide the KPI and FY 2024 Total. |
| 30 | Financial Modeling | 100.0% | 2/2 | pass | [what-is-the-maximum-dilutive-impact-in-number-of-shares-of-snapchat-s-ou](financial-research-agent/what-is-the-maximum-dilutive-impact-in-number-of-shares-of-snapchat-s-ou/) | What is the maximum dilutive impact in number of shares of Snapchat's outstanding convertible notes as of 12/… |
| 31 | Financial Modeling | 100.0% | 2/2 | pass | [assume-bros-grows-revenue-by-30-cagr-and-gross-margins-compress-by-500bp](financial-research-agent/assume-bros-grows-revenue-by-30-cagr-and-gross-margins-compress-by-500bp/) | Assume BROS grows revenue by 30% CAGR and gross margins compress by 500bps from YE 2024. What is BROS gross p… |
| 32 | Quantitative Retrieval | 100.0% | 3/3 | pass | [for-loandepot-nyse-ldi-what-is-the-breakdown-of-loan-originations-betwee](financial-research-agent/for-loandepot-nyse-ldi-what-is-the-breakdown-of-loan-originations-betwee/) | For loanDepot (NYSE: LDI) what is the breakdown of loan originations between purchases and refinancings for t… |
| 33 | Adjustments | 0.0% | 0/3 | fail | [what-would-be-the-impact-to-net-income-in-dollars-and-percent-if-all-deb](financial-research-agent/what-would-be-the-impact-to-net-income-in-dollars-and-percent-if-all-deb/) | What would be the impact to net income in dollars and percent if all debt for Boeing in 2024 were refinanced… |
| 34 | Quantitative Retrieval | 100.0% | 2/2 | pass | [in-fiscal-2024-what-percentage-of-cloudflare-s-nyse-net-revenue-were-der](financial-research-agent/in-fiscal-2024-what-percentage-of-cloudflare-s-nyse-net-revenue-were-der/) | In fiscal 2024, what percentage of Cloudflare's (NYSE: NET) revenue were derived from channel partners? |
| 35 | Adjustments | 100.0% | 2/2 | pass | [for-the-fiscal-year-ended-12-31-2023-what-was-uber-s-nyse-uber-largest-a](financial-research-agent/for-the-fiscal-year-ended-12-31-2023-what-was-uber-s-nyse-uber-largest-a/) | For the fiscal year ended 12/31/2023, what was Uber's (NYSE: UBER) largest adjustment to EBITDA. Provide the… |
| 36 | Quantitative Retrieval | 100.0% | 4/4 | pass | [what-price-was-rdfn-acquired-at-include-price-per-share-equity-value-and](financial-research-agent/what-price-was-rdfn-acquired-at-include-price-per-share-equity-value-and/) | What price was RDFN acquired at? (include price per share, equity value and enterprise value) |
| 37 | Quantitative Retrieval | 100.0% | 2/2 | pass | [as-of-dec-31-2024-what-was-warner-bros-discovery-s-nasdaq-wbd-total-rest](financial-research-agent/as-of-dec-31-2024-what-was-warner-bros-discovery-s-nasdaq-wbd-total-rest/) | As of Dec 31, 2024, what was Warner Bros. Discovery's (NASDAQ: WBD) Total Restructuring Costs incurred as a r… |
| 38 | Beat or Miss | 100.0% | 2/2 | pass | [how-did-lyft-s-q4-24-adjusted-ebitda-margin-adjusted-ebitda-gross-bookin](financial-research-agent/how-did-lyft-s-q4-24-adjusted-ebitda-margin-adjusted-ebitda-gross-bookin/) | How did Lyft's Q4'24 Adjusted EBITDA margin (adjusted EBITDA / Gross Bookings) compare to management guidance… |
| 39 | Qualitative Retrieval | 100.0% | 7/7 | pass | [what-financial-metrics-does-delta-airlines-nyse-dal-guide-on-in-its-quar](financial-research-agent/what-financial-metrics-does-delta-airlines-nyse-dal-guide-on-in-its-quar/) | What financial metrics does Delta Airlines (NYSE: DAL) guide on in its quarterly earnings reports? |
| 40 | Adjustments | 100.0% | 8/8 | pass | [what-adjustments-does-airbnb-nasdaq-abnb-make-to-its-net-income-to-deriv](financial-research-agent/what-adjustments-does-airbnb-nasdaq-abnb-make-to-its-net-income-to-deriv/) | What adjustments does Airbnb (NASDAQ: ABNB) make to its Net Income to Derive Adjusted EBITDA? |
| 41 | Quantitative Retrieval | 100.0% | 2/2 | pass | [what-was-fnd-same-store-sales-growth-in-q4-2024](financial-research-agent/what-was-fnd-same-store-sales-growth-in-q4-2024/) | What was FND same-store sales growth in Q4 2024? |
| 42 | Market Analysis | 50.0% | 3/6 | fail | [compare-the-fy24-dividend-payout-ratio-of-coca-cola-ko-to-that-of-its-co](financial-research-agent/compare-the-fy24-dividend-payout-ratio-of-coca-cola-ko-to-that-of-its-co/) | Compare the FY24 dividend payout ratio of Coca-Cola (KO) to that of its competitors and rank in order from hi… |
| 43 | Financial Modeling | 100.0% | 10/10 | pass | [what-portion-of-uber-s-2024-revenue-growth-was-driven-by-take-rate-expan](financial-research-agent/what-portion-of-uber-s-2024-revenue-growth-was-driven-by-take-rate-expan/) | What portion of Uber’s 2024 revenue growth was driven by take-rate expansion versus volume growth? |
| 44 | Quantitative Retrieval | 100.0% | 2/2 | pass | [in-2024-what-was-the-average-nights-per-booking-for-airbnb-nasdaq-abnb-i](financial-research-agent/in-2024-what-was-the-average-nights-per-booking-for-airbnb-nasdaq-abnb-i/) | In 2024, what was the Average Nights per Booking for Airbnb (NASDAQ: ABNB) in the Asia Pacific region? |
| 45 | Adjustments | 100.0% | 2/2 | pass | [in-2024-what-was-airbnb-s-nasdaq-abnb-adjustment-for-stock-based-compens](financial-research-agent/in-2024-what-was-airbnb-s-nasdaq-abnb-adjustment-for-stock-based-compens/) | In 2024, what was Airbnb's (NASDAQ: ABNB) adjustment for Stock-based Compensation Expense? |
| 46 | Market Analysis | 28.6% | 2/7 | fail | [as-of-december-2024-what-has-been-zillow-s-nasdaq-z-acquisition-strategy](financial-research-agent/as-of-december-2024-what-has-been-zillow-s-nasdaq-z-acquisition-strategy/) | As of December 2024, what has been Zillow's (NASDAQ:Z) acquisition strategy over the past 2 years and how doe… |
| 47 | Beat or Miss | 100.0% | 2/2 | pass | [did-four-beat-or-miss-its-end-to-end-payment-volume-guidance-at-midpoint](financial-research-agent/did-four-beat-or-miss-its-end-to-end-payment-volume-guidance-at-midpoint/) | Did FOUR beat or miss its end to end payment volume guidance at midpoint for Q3 2024 provided in Q1 2024? Exp… |
| 48 | Beat or Miss | 87.5% | 7/8 | fail | [how-did-lemonade-insurance-fy2024-results-compare-to-the-prior-quarter-s](financial-research-agent/how-did-lemonade-insurance-fy2024-results-compare-to-the-prior-quarter-s/) | How did Lemonade Insurance FY2024 results compare to the prior quarter's full year guidance? |
| 49 | Beat or Miss | 100.0% | 8/8 | pass | [in-fy23-and-fy24-did-general-mills-beat-or-miss-beginning-of-year-organi](financial-research-agent/in-fy23-and-fy24-did-general-mills-beat-or-miss-beginning-of-year-organi/) | In FY23 and FY24, did General Mills beat or miss beginning of year organic net sales growth guidance? What is… |
| 50 | Beat or Miss | 0.0% | 0/6 | fail | [by-how-much-did-amd-beat-miss-its-non-gaap-gross-profit-guide-implied-by](financial-research-agent/by-how-much-did-amd-beat-miss-its-non-gaap-gross-profit-guide-implied-by/) | By how much did AMD beat/miss its non-GAAP gross profit guide (implied by its non-GAAP gross margin guidance… |

## What this baseline means

This is a public, reproducible baseline for a financial research eval pack. It shows that AgentV can take a domain-specific dataset and rubric shape, run a web/coding agent target, produce per-case artifacts, and expose granular grader evidence without building a custom evaluation framework for this domain.

It is **not** a production merge gate and should not be read as investment advice or a claim that the target is ready for financial decision-making. Future gates should pin the target/model configuration, define explicit thresholds, decide how to handle time-sensitive benchmark drift, and run repeat trials before treating the numbers as release criteria.

## Limitations and caveats

- Finance facts are time-sensitive. A failure can indicate target error, stale reference data, or a mismatch between a pinned historical answer and later public filings/news.
- LLM-as-judge grading is useful for rubric traceability, but it is still probabilistic and should be reviewed for high-stakes claims.
- The benchmark covers 50 public questions, not the full space of financial analysis workflows.
- The public artifact intentionally omits provider endpoints, API keys, local logs, and exact runtime model environment values.
