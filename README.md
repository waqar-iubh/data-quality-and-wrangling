# Ask a Manager Salary Survey Data Tidying - Jupyter Notebook

## Overview

This Jupyter Notebook implements data tidying techniques for the *Ask a Manager Salary Survey* dataset, as described in the accompanying project report. The dataset, containing nearly 28,000 self-reported entries of salary and demographic information, is processed to address issues like inconsistent job titles, multi-currency salaries, outliers, and fragmented location data. The notebook applies fuzzy matching, feature construction, outlier capping, and feature aggregation to produce a clean, analysis-ready dataset.

## Dataset

- **Source**: [Ask a Manager Salary Survey 2021](https://www.kaggle.com/datasets/masoomaalghawas/ask-a-manager-salary-survey-2021) (Alghawas, 2021)
- **Input File**: `dataset.csv` (place in the same directory as the notebook)
- **Output File**: `processed_dataset.csv` (generated after running the notebook)

## Requirements

To run the notebook, install the required Python packages using:

```bash
pip install pandas numpy fuzzywuzzy python-Levenshtein
```

## Dependencies
- Python 3.6+
- pandas
- numpy
- fuzzywuzzy
- python-Levenshtein

## Notebook Structure
The notebook is organized into sections corresponding to the data tidying techniques described in the project report:

### Loading the Dataset
- Reads `dataset.csv` into a pandas DataFrame and displays its initial shape.

### Standardizing Job Titles using Fuzzy Matching
- Cleans job titles (lowercase, removes special characters).
- Applies fuzzy matching with fuzzywuzzy’s `token_sort_ratio` to standardize variations (e.g., "Project Manager" vs. "Proj Mgr").
- Outputs a new column: `standardized_Job title`.

### Feature Construction for Adjusted Salary
- Converts salaries and bonuses to USD using predefined exchange rates.
- Adjusts for Purchasing Power Parity (PPP) to create `Salary in USD (PPP Adjusted)`.
- Handles missing or malformed values.

### Outlier Handling
- Caps extreme values in `Salary in USD (PPP Adjusted)` at the 95th percentile.
- Creates a new column: `Salary in USD (Capped)`.

### Feature Aggregation for Location
- Standardizes country names (e.g., "United States" to "USA").
- Combines country, state, and city into a single `Location` column (e.g., "USA-Massachusetts-Boston" or "Canada-Toronto").

### Saving the Processed Dataset
- Exports the tidied dataset to `processed_dataset.csv`.

## Usage
### Prepare the Dataset
- Download the dataset from Kaggle and save it as `dataset.csv` in the same directory as the notebook.
- Ensure the column names match those expected (e.g., "Job title", "Annual salary", "Currency", "What country do you work in?").

### Run the Notebook
- Open the notebook in Jupyter or a compatible environment (e.g., VS Code, Google Colab).
- Execute the cells sequentially to process the dataset.
- Monitor outputs to verify each step (e.g., number of unique job titles reduced, max capped salary).

### Output
- The notebook generates `processed_dataset.csv` with new columns: `standardized_Job title`, `Salary in USD`, `Salary in USD (PPP Adjusted)`, `Salary in USD (Capped)`, and `Location`.

## Notes
- **Exchange Rates and PPP Factors**: The notebook uses approximate conversion rates and PPP factors as of April 2025. Update these in the `conversion_rates` and `ppp_factors` dictionaries for accuracy.
- **Performance**: Fuzzy matching on large datasets may be slow; adjust the threshold parameter (default: 50) to balance accuracy and speed.
- **Error Handling**: The code includes basic checks for missing files and malformed data. If errors occur, verify the input CSV’s structure.
- **Extensibility**: The functions are modular and can be adapted for other datasets with similar issues (e.g., free-text fields, multi-unit numerical data).

## References
- Alghawas, M. (2021). *Ask a Manager Salary Survey 2021* [Data set]. Kaggle. [https://www.kaggle.com/datasets/masoomaalghawas/ask-a-manager-salary-survey-2021](https://www.kaggle.com/datasets/masoomaalghawas/ask-a-manager-salary-survey-2021)
