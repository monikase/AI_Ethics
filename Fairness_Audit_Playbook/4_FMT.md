# Fairness Metrics Tool (FMT)
## Quantitative Fairness Implementation Framework

---

## 1. Purpose

The Fairness Metrics Tool (FMT) provides a structured methodology for translating selected fairness definitions into measurable, statistically valid, and intersectionally robust evaluation metrics.

It ensures that fairness:

- Is quantitatively defined rather than intuitively assumed
- Is validated with statistical rigor
- Accounts for intersectional subgroup risk
- Is robust to sampling variation
- Produces actionable governance outputs

FMT is applied after:

1. Historical Context Assessment  
2. Fairness Definition Selection  
3. Bias Source Identification  

---

## 2. Metric Selection Framework

### Step 1: Identify Problem Type

- Classification
- Regression
- Ranking

---

### Step 2: Map Fairness Definitions to Metrics

#### Classification Systems

| Fairness Definition | Primary Metric |
|---------------------|----------------|
| Demographic Parity | Statistical Parity Difference (SPD) |
| Equal Opportunity | True Positive Rate Difference (EOD) |
| Equalized Odds | TPR + FPR Differences |
| Predictive Parity | Positive Predictive Value Difference |
| Individual Fairness | Similarity Violation Rate |
| Counterfactual Fairness | Counterfactual Prediction Gap |

Additional rule:
- If False Negatives are more harmful → prioritize TPR / FNR disparity.
- If False Positives are more harmful → prioritize FPR disparity.

---

#### Regression Systems

| Fairness Definition | Metric |
|---------------------|--------|
| Statistical Parity | Mean Outcome Difference |
| Bounded Group Loss | Maximum Group Error |
| Individual Fairness | Input–Output Sensitivity |

Error direction:
- Overprediction harm → Positive Residual Difference
- Underprediction harm → Negative Residual Difference
- Both → Absolute Residual Difference

---

#### Ranking Systems

| Fairness Definition | Metric |
|---------------------|--------|
| Exposure Parity | Exposure Ratio |
| Representation Parity | Top-k Proportion Difference |
| Individual Fairness | Rank Consistency Score |

---

## 3. Intersectional Extension

For every selected metric:

1. Compute across individual protected attributes.
2. Compute across all relevant attribute intersections.
3. Identify worst-case subgroup disparity.
4. Check for Simpson’s Paradox (aggregate fairness masking subgroup disparity).

Intersectional evaluation is mandatory for high-risk systems.

---

## 4. Statistical Validation Protocol

### 4.1 Uncertainty Quantification

For each metric:

- Compute point estimate.
- Generate 95% confidence interval using bootstrap (≥ 5,000 resamples).
- Report interval alongside point estimate.

---

### 4.2 Hypothesis Testing

- Null hypothesis: No disparity.
- Compute p-value.
- Apply multiple testing correction (Benjamini–Hochberg).
- Report both p-value and effect size.

---

### 4.3 Small Sample Handling

If subgroup size < 100:

- Use Bayesian estimation with weakly informative priors.
- Report 95% credible intervals.
- Flag high uncertainty.
- Avoid definitive fairness claims.

If subgroup extremely small:
- Document limitation.
- Recommend targeted data collection.

---

## 5. Robustness Verification

Fairness findings must be stable across:

- Cross-validation splits
- Temporal splits (if available)
- Threshold sensitivity testing
- Moderate distribution shifts

Disparities that fluctuate significantly must be flagged as unstable.

---

## 6. Visualization & Reporting Templates

### 6.1 Fairness Disparity Chart

- Bar chart of disparity values by group
- Error bars = 95% CI
- Red highlight if statistically significant
- Horizontal threshold reference line

---

### 6.2 Intersectional Heatmap

- Rows = intersectional subgroups
- Columns = selected metrics
- Color = disparity magnitude
- Annotation = sample size

---

### 6.3 Governance Summary Table

| Metric | Disparity | 95% CI | p-value | Significant | Robust | Action |
|--------|-----------|--------|--------|------------|--------|--------|

---

## 7. Decision Escalation Rules

Disparities require mitigation if:

- Statistically significant after correction
- Exceed predefined threshold
- Robust across validation splits
- Aligned with historical risk patterns

All decisions must be documented.

---

## 8. Output Requirements

Each evaluation must include:

- Selected fairness definitions
- Metrics implemented
- Statistical validation results
- Intersectional findings
- Robustness assessment
- Intervention decision
- Monitoring plan

Fairness claims without statistical validation are invalid.
