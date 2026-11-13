# Proposal

## Hypothesis

A negative binomial regression using historical bicycle-rental counts and calendar patterns can reduce next-hour capacity-planning loss compared with a same-hour previous-week seasonal baseline. The forecast quantity is **recorded Capital Bikeshare rentals during the next hour**, measured in rentals per hour across the Washington, DC system.

## Data

The project uses the UCI Bike Sharing Dataset (DOI: 10.24432/C5W894), specifically `hour.csv`, containing approximately 17,000 hourly records from 2011–2012. Each observation records completed rentals, calendar information, and weather descriptors. The exact sample size and SHA-256 checksum will be verified from the downloaded CSV. The dataset is distributed under CC BY 4.0 with attribution.

The analysis uses chronological training, validation, and held-out test periods. Only information available before the forecast hour will be used. Recorded completed rentals may underestimate underlying customer demand because unsuccessful rental attempts are not observed. Therefore, the capacity target and evaluation concern **recorded rentals only**, not unobserved unmet demand.

## Decision affected by the model

A hypothetical system-wide bike-sharing planner selects an hourly capacity target \(q\). The observed outcome \(D\) is the number of recorded completed rentals.

The illustrative loss is:

\[
L(q,D)=4\max(D-q,0)+\max(q-D,0).
\]

The shortage cost is \(c_s=4\) and the excess-capacity cost is \(c_e=1\), giving a **4:1 shortage-to-excess cost ratio**, measured in hypothetical loss units per rental. Under this loss, the optimal capacity is the **80th percentile of the negative binomial predictive distribution**, subject to clarification of the quantile notation in the GitHub issue.

The named seasonal baseline is the **recorded rental count from the same hour seven days earlier**. Both methods will be scored on identical chronologically held-out hours using average asymmetric loss units per hour. Simulation, calibration, residual analysis, and cost sensitivity will assess model behavior. Open-Meteo remains a clearly labeled demonstration rather than a validated present-day rental forecast.
