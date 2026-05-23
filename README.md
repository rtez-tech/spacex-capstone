# SpaceX Falcon 9 First Stage Landing Prediction

**IBM Data Science Professional Certificate — Applied Data Science Capstone**
Author: Roberto Cortez · GitHub: [@rtez-tech](https://github.com/rtez-tech)

Predicting whether the Falcon 9 first stage will land successfully, so the true
cost of a launch can be estimated. SpaceX advertises Falcon 9 launches at ~$62M
versus ~$165M for competitors, largely because it reuses the first stage —
so predicting landings predicts cost.

## Repository contents

| File | Description |
|------|-------------|
| `notebooks/1_spacex_data_collection_api.ipynb` | Collect launch data from the SpaceX REST API |
| `notebooks/2_spacex_web_scraping.ipynb` | Scrape launch records from Wikipedia with BeautifulSoup |
| `notebooks/3_spacex_data_wrangling.ipynb` | Build the binary landing-success label (`Class`) |
| `notebooks/4_spacex_eda_sql.ipynb` | EDA with SQL (10 analytical queries) |
| `notebooks/5_spacex_eda_visualization.ipynb` | EDA with visualization + feature engineering |
| `notebooks/6_spacex_folium_map.ipynb` | Interactive Folium map of launch sites & outcomes |
| `notebooks/7_spacex_dash_app.ipynb` | Builds the Plotly Dash dashboard (`spacex_dash_app.py`) |
| `notebooks/8_spacex_predictive_analysis.ipynb` | Train, tune & evaluate four classifiers |
| `spacex_dash_app.py` | Standalone Plotly Dash application |
| `SpaceX_Capstone_Roberto_Cortez.pptx` | Final presentation (export to PDF for submission) |

## Setup

```bash
python3 -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate
pip install -r requirements.txt
```

`requirements.txt`:

```
pandas
numpy
requests
beautifulsoup4
matplotlib
seaborn
scikit-learn
folium
plotly
dash
ipython-sql
sqlalchemy
jupyter
```

## How to run

1. **Run the notebooks in order, 1 → 8.** Each one downloads the data it needs from
   the IBM course data sources (you need internet access). Notebooks 1, 3, and 5
   write CSV files that later notebooks read. Run top-to-bottom so the files exist.
2. **Launch the dashboard** (after running notebook 7, which writes the app + CSV):
   ```bash
   python3 spacex_dash_app.py
   ```
   Open <http://127.0.0.1:8050> in your browser.
3. **Capture screenshots** for the presentation:
   - Folium maps (notebook 6) → slides 35–37
   - Dash app → slides 39–41
4. **Verify your model numbers.** After running notebook 8, check the accuracy bar
   chart and confusion matrix against slides 43–44 and update the slides if your
   numbers differ (small differences are normal across scikit-learn versions).
5. **Export the presentation to PDF** before submitting to Coursera.

## Methodology summary

- **Data collection:** SpaceX REST API + Wikipedia web scraping
- **Wrangling:** map landing outcomes to a binary `Class` (1 = landed, 0 = not)
- **EDA:** SQL queries + seaborn visualizations
- **Interactive analytics:** Folium maps + Plotly Dash dashboard
- **Modeling:** Logistic Regression, SVM, Decision Tree, KNN — tuned with
  `GridSearchCV` (10-fold CV), compared on test accuracy, evaluated with a
  confusion matrix.

## Key findings

- Landing success climbed from near-zero in the early years to ~80–90% recently.
- KSC LC-39A is the strongest launch site; ES-L1 / GEO / SSO orbits show the
  highest success rates.
- Very heavy payloads (especially to GTO) are associated with lower success.
- The best classifier reaches ~83% accuracy; the main error mode is false positives.
