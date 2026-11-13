## 2026-11-12: Chronological evaluation and demonstration scope

- **Decision.** Use chronological training, validation, and held-out test periods for the recorded hourly rental series. The planned split is training before July 1, 2012; validation from July 1 through September 30, 2012; and testing from October 1 through December 31, 2012. Keep Open-Meteo as a demonstration of current weather information and illustrative scenarios, not a validated current-day rental forecast.
- **Why.** Chronological evaluation respects the ordering of observations and avoids training on future outcomes. The historical rental dataset does not establish present-day forecasting accuracy. Random simulation results will use seed 20261111 for reproducibility.
- **Alternative.** Random train/test splitting or presenting historical model outputs as live operational forecasts.
- **Revisit.** Reconsider the split if there is evidence of leakage or inadequate evaluation coverage. Reconsider live forecasting claims only after obtaining current rental data and conducting a separate out-of-sample validation.
