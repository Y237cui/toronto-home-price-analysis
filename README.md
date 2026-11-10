# Toronto Home-Price Prediction — Error Analysis & Statistical Evaluation

**SSU Data Dash 2026 · University of Toronto · Collaborative team project**

**Yan Cui** · [GitHub @Y237cui](https://github.com/Y237cui)  
**My primary contributions:** Training, Error analysis, interpretation of validation results, and technical report writing.

> **About this repository:** This is my personal academic portfolio overview of a collaborative competition project. The prediction models, code, experiments, and submission are team work. The [original team repository](https://github.com/billchenziang33/toronto-home-price-prediction-2026) remains the source of truth for implementation and reproducibility. A selected, attributed copy of the team's source files and reports is included in [`team_source/`](team_source/) for convenient inspection; it is **not a complete or independently runnable mirror**.

## Project overview

The SSU Data Dash 2026 challenge involved predicting residential sale prices from **synthetic Toronto-area housing data** in two settings:

- **Off-market:** Predict a home's sale price without a list price.
- **List-aware:** Predict sale price with a list price provided.

The team worked with approximately **150,000 synthetic historical transactions**, building gradient-boosting models and evaluating them through temporally ordered, month-by-month walk-forward validation.

## My contributions

### Error analysis and model diagnostics
- Investigated predictive errors across **price deciles, property types, and temporal segments**, identifying variation in model reliability.
- Examined **median absolute percentage error (MdAPE), mean absolute percentage error (MAPE), tail errors (P90 APE), and signed percentage error** to communicate complementary aspects of performance.
- Interpreted subgroup differences with attention to sample sizes and the limitations of synthetic data.

### Statistical interpretation
- Analyzed and communicated results from **six-month walk-forward validation** and comparisons of candidate model routes.
- Discussed the interpretation of **home-level bootstrap confidence intervals** and paired comparisons, including their limitations under shared monthly effects.
- Distinguished retrospective, repeatedly examined validation data from a fresh holdout or the competition's hidden test set.

### Technical reporting
- Contributed to writing the team's technical report, summarizing the validation methodology, predictive performance, error patterns, and limitations.
- Presented statistical findings and methodological caveats to support transparent communication of team results.

## Team validation results

The final team repository reports the following **retrospective walk-forward validation** results for December 2025–May 2026, based on **10,069 homes per track**:

| Track | Selected route | MdAPE | MAPE | P90 APE |
| --- | --- | ---: | ---: | ---: |
| Off-market | R52 | **7.07%** | 9.52% | 20.23% |
| List-aware | R97 | **3.94%** | 5.03% | 10.57% |

These are **team-level validation results**, not scores attributable to one person. The six-month validation window was used in model development; results should **not** be described as independent holdout or hidden-test performance.

For route comparisons and bootstrap intervals, see the [original validation report](https://github.com/billchenziang33/toronto-home-price-prediction-2026/blob/main/reports/validation_report.md).

## Error-analysis framework

For observed sale price $y_i>0$ and prediction $\hat{y}_i$, define absolute percentage error as

$$
\mathrm{APE}_i = 100\,\frac{|y_i-\hat{y}_i|}{y_i}.
$$

| Diagnostic | Interpretation |
| --- | --- |
| **MdAPE** | Median absolute percentage error; robust summary of typical relative error |
| **MAPE** | Mean absolute percentage error; more sensitive to large errors |
| **P90 APE** | 90th percentile of relative prediction error |
| **Signed error** | Direction and magnitude of over- or underprediction |
| **Segment-level error** | Variation across price deciles, property types, months, and communities |
| **Bootstrap confidence intervals** | Sampling variability of reported metrics and paired differences under home-level resampling |

The source report suppresses community-level metrics for groups with fewer than 30 observations.

## Statistical limitations

1. **Synthetic data:** Findings do not establish the performance of a real-world Toronto property valuation service.
2. **Retrospective validation:** The evaluation months were examined during development, so performance estimates may be optimistic after repeated model selection.
3. **Dependence:** Home-level bootstrap intervals do not fully capture correlations among sales within the same month.
4. **Descriptive comparisons:** Error differences by property or price segment do not establish causal explanations.

## Original source and team credit

- **[Original team repository — code, experiments, and reproducibility instructions](https://github.com/billchenziang33/toronto-home-price-prediction-2026)**
- **[Detailed validation report](https://github.com/billchenziang33/toronto-home-price-prediction-2026/blob/main/reports/validation_report.md)**
- **[Team competition report source](https://github.com/billchenziang33/toronto-home-price-prediction-2026/blob/main/report/report.tex)**

**Team:** Yan Cui, Jiayi Guan, Shengde Wang, and Ziang Chen (as listed in the team's report).

## Included team source snapshot

The [`team_source/`](team_source/) directory includes selected files copied from the original team's public repository:

- `run.py`, `data.py`, `features.py`, `models.py`, `submission_models.py`, `check_submission.py`: pipeline, feature processing, model, and validation utilities.
- `requirements.txt`: Python dependencies.
- `reports/validation_report.md`: retrospective validation and subgroup error analysis.
- `report/report.tex`: team-authored report source (an earlier draft; figures and generated tables are not bundled).
- `LICENSE`: the original project's MIT license and copyright statement.

**Important:** This selected snapshot does not include all model assets, generated output files, figures, and other dependencies required by the original submission. **Do not use it as a replacement for the complete team repository**; for reproducible predictions and current results, use the original repo linked above. The report source and the latest README refer to different stages of the team's development; the final selected routes and metrics are those given in the latest original README.

**Attribution:** The code and reports in `team_source/` are a copy of collaborative team material, not independent work authored solely by Yan Cui. The MIT license and original copyright notice are preserved in `team_source/LICENSE`. No model training or validation was executed as part of preparing this portfolio snapshot.
