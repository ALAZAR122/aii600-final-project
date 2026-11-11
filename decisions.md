# Decisions

This file is the history of the project. Append an entry when a choice changes the work: the quantity, the data, the split, the model, the loss, or the action. Leave old entries in place. A later entry can reverse an earlier one. If a result depends on a random draw, record the seed under Why. The split entry records the cutoff date, or the seed and the fraction. The pull request that merges the code names this entry.

## 2026-11-11: Select FlowCast AI Live for probabilistic demand forecasting

- Decision. Develop FlowCast AI Live to forecast next-hour Capital Bikeshare rentals in rentals/hour using the UCI Bike Sharing Dataset. Use negative binomial regression, compare it against a seasonal-naive baseline, and demonstrate optional live weather integration through Open-Meteo. Evaluate a hypothetical system-wide hourly capacity decision using asymmetric shortage and excess-capacity costs.

- Why. The public hourly rental dataset supports count regression, statistical simulation, uncertainty quantification, and chronological out-of-sample evaluation. The project connects predictive distributions to measurable hypothetical decision loss. Open-Meteo enables a low-cost live weather demonstration. Historical evaluation will avoid future-information leakage. Recorded rentals may underestimate unconstrained demand, so the analysis will not claim verified operational savings.

- Alternative. Rejected AURA AI, an air-quality forecasting and alert system, because FlowCast offers a more direct connection between predictions, mathematical decisions, and measurable loss. Also rejected a point-forecast-only approach because it would not adequately represent decision uncertainty.

- Revisit. Reconsider the approach if data validation fails, negative binomial regression is poorly calibrated, the seasonal baseline performs better in held-out decision loss, or the API integration compromises reproducibility. Record the actual split cutoff dates and simulation seeds in subsequent entries.
