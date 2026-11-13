## 2026-11-12: Specify numerical loss and seasonal baseline

- **Decision.** Use a 4:1 shortage-to-excess cost ratio, with shortage cost 4 and excess-capacity cost 1 hypothetical loss unit per recorded rental. Use the 80th percentile of the negative binomial predictive distribution as the hourly capacity target. Compare against the recorded rental count from the same hour seven days earlier.
- **Why.** Professor feedback requires numerical costs, an explicit capacity quantile, a named seasonal baseline, and held-out evaluation using the same loss. The observed outcome is recorded completed rentals, not unobserved customer demand.
- **Alternative.** Equal shortage and excess costs, resulting in median-based capacity; a Poisson model may also serve as a secondary statistical comparison.
- **Revisit.** Revise the cost ratio if credible operational estimates become available. Reconsider the model if held-out loss or calibration is poor. Clarify the quantile notation in the professor's GitHub issue before finalizing the analysis.
