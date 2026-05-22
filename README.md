# IBM Data Science Professional Certificate — Capstone

Notebooks I built while earning the **IBM Data Science Professional Certificate** on Coursera. The headline project is the **Applied Data Science Capstone** — predicting whether a SpaceX **Falcon 9** first stage will land successfully — with a separate Data Analysis with Python module on King County house sales.

If the first stage lands, the launch costs ≈ \$62M instead of the ≈ \$165M competitors charge. A reliable landing-prediction model is therefore a useful input for anyone bidding against SpaceX.

---

## Notebooks

| Notebook | What it does |
|---|---|
| [`Data Collection API.ipynb`](Data%20Collection%20API.ipynb) | Pulls Falcon 9 launch history from the **SpaceX REST API** (`api.spacexdata.com/v4`), resolves rocket / payload / launchpad / core IDs, normalizes nested JSON with `json_normalize`, filters to Falcon 9 launches, handles missing `PayloadMass`, and writes `dataset_part_1.csv`. |
| [`Data Collection with Web Scraping.ipynb`](Data%20Collection%20with%20Web%20Scraping.ipynb) | Scrapes the **Falcon 9 launch records** table from Wikipedia with `requests` + `BeautifulSoup` as a second, independent source for cross-validation. |
| [`EDA.ipynb`](EDA.ipynb) | Exploratory analysis on the merged launch dataset — launches per site, orbit distribution, and **landing-outcome label engineering** (`True ASDS / True RTLS / True Ocean` → `1`, otherwise `0`). Exports `dataset_part_2.csv` for the modeling stage. |
| [`peer-graded assignment.ipynb`](peer-graded%20assignment.ipynb) | Separate module — **King County (Seattle) house-price regression**. Linear regression, multivariate features, `Pipeline` with `StandardScaler` + `PolynomialFeatures`, and a Ridge model (degree-2 polynomial) reaching R² ≈ 0.70 on the test split. |

---

## Stack

- **Python** — Pandas, NumPy, requests, BeautifulSoup
- **Visualization** — Matplotlib, Seaborn
- **Modeling** — scikit-learn (`LinearRegression`, `Ridge`, `Pipeline`, `PolynomialFeatures`, `StandardScaler`)
- **Course platform** — IBM Skills Network / Coursera

---

## Pipeline (SpaceX capstone)

```
SpaceX API ─┐
            ├──> clean + normalize ──> Wikipedia scrape (cross-check)
            │                                    │
            └────────────────┬───────────────────┘
                             ▼
                       merged dataset
                             │
                             ▼
                     EDA + label engineering   (landing success = 1/0)
                             │
                             ▼
                  classification model (next stage)
```

---

## Running the notebooks

```bash
pip install pandas numpy requests beautifulsoup4 scikit-learn matplotlib seaborn jupyter
jupyter notebook
```

Open any of the `.ipynb` files and run top-to-bottom. The API + scrape notebooks write their CSV outputs into the working directory; the EDA notebook reads them back in.

---

*Coursework adapted from the **IBM Data Science Professional Certificate** on Coursera (© IBM Corporation).*
