# UCI hourly bike-sharing data

- **Source:** UCI Machine Learning Repository, Bike Sharing Dataset, DOI: 10.24432/C5W894.
- **File:** `hour.csv` inside the official dataset ZIP.
- **Unit:** completed rentals per recorded hour in the Capital Bikeshare system.
- **Observed sample:** 17,379 rows spanning 2011-01-01 through 2012-12-31.
- **Retrieval:** the notebook's Data cell downloads `https://archive.ics.uci.edu/static/public/275/bike+sharing+dataset.zip` and extracts `hour.csv` into `data/`. No raw data files are committed to git.
- **License/attribution:** review UCI's dataset terms before redistribution; this repository uses an official-source download instead of republishing the CSV.

## SHA-256 verification — REQUIRED BEFORE MARKING REPRODUCIBLE

Run the Data cell of `analysis.ipynb`, which prints the SHA-256 of `data/hour.csv`. Paste the actual 64-character digest into the entry below, then verify it against a fresh download. **No checksum has been invented here.**

`hour.csv SHA-256: [TO BE RECORDED FROM VERIFIED DOWNLOAD]`

Once the digest is known, the notebook should assert that the downloaded bytes match it before training.
