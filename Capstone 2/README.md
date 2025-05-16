# SD_RIPA_StopDuration

This project investigates stop duration patterns using the San Diego Police Department’s RIPA (Racial and Identity Profiling Act) dataset. My goal is to identify which factors influence the length of police stops and build a predictive model to estimate stopduration in minutes.

The San Diego RIPA dataset is available from the City of San Diego Open Data Portal:  
👉 https://data.sandiego.gov/datasets/police-ripa-stops/

---

In `ripa_data_wrangling.ipynb`, I merged the base stop dataset (`ripa_stops_historic.csv`) with 14 supplementary tables, including officer-perceived gender, race, search basis, and stop outcomes. These are joined on the `uid` field to create a fully enriched dataset ready for cleaning.

In `ripa_eda.ipynb`, I explored key trends in stopduration. I observed that most stops last under 20 minutes, but longer durations are associated with contraband found, arrests made, and certain demographic profiles. Officer-perceived race and gender appear to correlate with stop length, particularly for Hispanic/Latino and male individuals.

In `ripa_preprocessing.ipynb`, I transformed the data for modeling:
- Parsed timestamps into `stop_hour` and `time_of_day` bins
- One-hot encoded categorical variables
- Standardized numerical variables
- Imputed missing values
- Applied feature pruning using `SelectFromModel` with Random Forest

In `ripa_modeling.ipynb`, I trained and evaluate five models:
- Dummy Regressor  
- Linear Regression  
- Ridge Regression  
- Random Forest Regressor  
- K-Nearest Neighbors (sampled for efficiency)

Among these, the Random Forest model achieves the best results:
- **Test RMSE:** 41.57  
- **Test R²:** 0.334  
- **Train R²:** 0.489  
- **Bootstrapped R² Range:** 0.320 – 0.331 (20 runs)

Although overall predictive performance is moderate, the model is stable and interpretable. It highlights patterns that can help support fairness and transparency in traffic stop outcomes.

---

## File Structure

| File                          | Purpose                                          |
|-------------------------------|--------------------------------------------------|
| `ripa_data_wrangling.ipynb`   | Merges all RIPA data into a single dataset       |
| `ripa_eda.ipynb`              | Explores patterns in stopduration                |
| `ripa_preprocessing.ipynb`    | Cleans and encodes data for modeling             |
| `ripa_modeling.ipynb`         | Builds and evaluates models                      |
| `model_metrics.txt`           | Final model summary (Random Forest)              |
| `Capstone_Final_Report.pdf`   | Written summary and interpretation               |

---
