## 2026-11-12: Chronological evaluation and demonstration scope

- **Decision.** Use chronological training, validation, and held-out test periods for the recorded hourly rental series. The planned split is training before July 1, 2012; validation from July 1 through September 30, 2012; and testing from October 1 through December 31, 2012. Keep Open-Meteo as a demonstration of current weather information and illustrative scenarios, not a validated current-day rental forecast.
- **Why.** Chronological evaluation respects the ordering of observations and avoids training on future outcomes. The historical rental dataset does not establish present-day forecasting accuracy. The original planning entry named seed 20261111; the executed notebook uses seed 20261112, documented in a later entry.
- **Alternative.** Random train/test splitting or presenting historical model outputs as live operational forecasts.
- **Revisit.** Reconsider the split if there is evidence of leakage or inadequate evaluation coverage. Reconsider live forecasting claims only after obtaining current rental data and conducting a separate out-of-sample validation.

## 2026-11-20: Implement the hourly NB2 forecast

- **Decision.** Fit an NB2 negative binomial regression on the chronological training subset using cyclical calendar terms, weekend indicator, and the observed rental counts from 1, 24, and 168 hours earlier (log-transformed lag predictors). Model mean is `exp(X beta)` and conditional variance is `mu + alpha * mu**2`.
- **Why.** Hourly completed-rental counts are nonnegative and show overdispersion; NB2 allows variance above the conditional mean. The notebook fits the model only to training rows.
- **Alternative.** A Poisson count model or a point forecast without an estimated count distribution.
- **Revisit.** Refit or reconsider if lag inputs are unavailable at decision time, dispersion diagnostics fail, or later out-of-time data contradict historical performance.

## 2026-11-20: Use a previous-week capacity baseline

- **Decision.** Compare model capacity to the recorded rental count at the same hour 168 hours earlier.
- **Why.** It is simple, reproducible, and respects recurring weekly patterns; it is scored using the same held-out loss as the NB2 decision.
- **Alternative.** A global-mean baseline or a baseline assessed only with RMSE.
- **Revisit.** Add stronger seasonal or operational baselines if new data or project time permits.

## 2026-11-20: Specify asymmetric loss and rental-count quantile

- **Decision.** Use `L(q,D) = 4*max(D-q,0) + max(q-D,0)` for nonnegative integer capacity `q` and observed completed-rental count `D`. The 4 and 1 are illustrative shortage and excess-capacity penalties in weighted loss units per rental. Choose the smallest integer `q` with fitted NB2 predictive CDF `F(q) >= 4/(4+1) = 0.8`.
- **Why.** This rule minimizes expected asymmetric loss under the fitted discrete predictive distribution. The quantile is a quantile of the **predicted rental-count distribution**, not the empirical 80th percentile of the dataset.
- **Alternative.** Rounded predicted mean, symmetric loss, or an arbitrary fixed capacity.
- **Revisit.** Change the rule when empirical operational shortage/excess costs, true unmet demand, or capacity constraints become available.

## 2026-11-20: Evaluate on the held-out 2012 period

- **Decision.** Report October–December 2012 held-out mean weighted decision loss, simulation, residuals, and predictive calibration.
- **Why.** Saved notebook outputs show 2,098 test hours, NB2 quantile loss 105.601 and previous-week baseline loss 149.752 weighted loss units/hour, a 29.48% reduction. Nominal 90% interval coverage is approximately 91%. The model also has 1,014 hourly wins, 22 ties, and 1,062 losses versus the baseline; aggregate loss, not win count, determines the preferred strategy under the stated loss.
- **Alternative.** In-sample fit alone or reporting only MAE/RMSE.
- **Revisit.** Recalculate after a clean top-to-bottom execution, changes to model or data, or new independent historical periods.
- **Seed.** The executed notebook records `20261112` for stochastic experiments.
- **Limitation.** Observed completed rentals are not total latent demand; no actual operational costs or monetary savings are demonstrated.
