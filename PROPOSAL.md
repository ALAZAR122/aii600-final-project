# Proposal

## Hypothesis

A probabilistic model using historical bicycle rentals and calendar patterns can reduce expected hourly capacity-planning loss compared with a seasonal baseline. The target is **total Capital Bikeshare rentals in the next hour**, measured in rentals/hour across Washington, DC.

## Data

The project uses the **UCI Bike Sharing Dataset** (DOI: 10.24432/C5W894), containing 17,379 hourly records from 2011–2012. Each observation represents completed bicycle rentals during one hour, collected from Capital Bikeshare records and supplemented with calendar and weather information.

An **Open-Meteo live weather API** will provide current temperature, precipitation, and wind forecasts for an interactive prototype. Historical model evaluation will use only information available before each forecast hour; current API data will support a clearly labeled demonstration rather than claims of validated present-day accuracy.

Completed rentals may underestimate actual customer demand when bicycles are unavailable, creating potential downward bias. The dataset does not include unmet requests or actual capacity. UCI distributes the dataset under **CC BY 4.0**, permitting redistribution with attribution. Data sources, download commands, and SHA-256 checksums will be documented in `data/README.md`.

## Decision affected by the model

A hypothetical bike-sharing operations planner will use the predictive distribution to choose a **system-wide hourly rental-service capacity target**, minimizing expected shortage and excess-capacity costs.

The decision loss is:

**L(q,D) = cₛ max(D − q, 0) + cₑ max(q − D, 0)**

Here, `q` is planned capacity, `D` is recorded rentals, and `cₛ > cₑ`, meaning unmet modeled demand is costlier than unused capacity.

A negative binomial regression will be compared with a seasonal baseline using chronological held-out data, predictive calibration, simulated parameter recovery, and decision loss. Python-based visualizations and an optional live API dashboard will demonstrate forecast uncertainty, risk sensitivity, and the hypothetical value of better predictions.
