# Tamil Nadu 2026 Election Result Analysis

A mini project for **Framework for Data Visual Analytics (FDVA)** focused on exploring and visualizing the 2026 Tamil Nadu Legislative Assembly election results using Python, Power BI, and Tableau.

## Project Overview

This project analyzes election-result data to understand constituency-level outcomes, party performance, candidate vote counts, and patterns across Tamil Nadu. Python is used for data cleaning and exploratory analysis, while Power BI and Tableau are used to build interactive dashboards.

> **Data note:** Verify all figures against the CSV dataset and an official election source before presenting or publishing results. Do not treat illustrative charts or unverified values as official results.

## Objectives

- Load and inspect the election dataset in CSV format.
- Clean column names, text values, numeric vote fields, and missing values.
- Explore party-wise and constituency-wise results.
- Visualize vote counts, winning candidates, party performance, and constituency-level patterns.
- Build interactive dashboards in Power BI and Tableau.
- Present key findings clearly and transparently.

## Tools and Technologies

- **Python** — data preparation and analysis
- **Pandas** — data loading and cleaning
- **Matplotlib / Seaborn** — charts and exploratory visualization
- **Power BI** — interactive dashboard
- **Tableau** — interactive dashboard
- **CSV** — input data format

## Dataset

Place the election results CSV file in the project folder, or update the file path in the notebook/script.

Suggested fields, depending on the dataset available:

- Constituency
- Candidate name
- Political party
- Votes received
- Vote share
- Winning status
- Winning margin

The actual column names may differ by source. Check the CSV headers before running any analysis. Do not assume fields exist if they are absent from the downloaded dataset.

## Project Structure

```text
Tamil-Nadu-2026-Election-Result/
├── data/
│   └── election_results.csv
├── notebooks/
│   └── election_analysis.ipynb
├── charts/
│   └── (generated visualizations)
├── powerbi/
│   └── (Power BI report file)
├── tableau/
│   └── (Tableau workbook)
└── README.md
```

This is a suggested structure; adjust the filenames and folders to match the files in your project.

## Getting Started

### 1. Requirements

Install Python 3 and the libraries used for analysis:

```bash
pip install pandas matplotlib seaborn jupyter
```

### 2. Add the dataset

Download the Tamil Nadu 2026 election-results CSV from a reliable source and place it in the `data/` folder. Update the path in your code if the file has a different name or location.

### 3. Load and inspect the data

```python
import pandas as pd

df = pd.read_csv("data/election_results.csv")

print(df.head())
print(df.shape)
print(df.info())
print(df.isnull().sum())
```

### 4. Clean and prepare the data

Review missing values, duplicates, inconsistent text labels, and data types. Convert vote counts and other numeric fields to numeric types only after checking for commas, symbols, or other formatting. Do not fill missing election results without a documented reason.

```python
df.columns = df.columns.str.strip()
df = df.drop_duplicates()

# Example only: change this list to match your CSV's real column names.
for column in ["Votes"]:
    if column in df.columns:
        df[column] = pd.to_numeric(
            df[column].astype(str).str.replace(",", "", regex=False),
            errors="coerce"
        )

print(df.isnull().sum())
```

### 5. Explore and visualize

Create charts only for columns present in the dataset. Useful options include:

- Seats won by political party
- Votes by party
- Top candidates by votes
- Constituency-wise winning margins
- Vote share by party
- Constituency-level geographic visualization, if reliable geographic data is available

Example party-wise vote chart (update `Party` and `Votes` if your CSV uses different column names):

```python
import matplotlib.pyplot as plt

if {"Party", "Votes"}.issubset(df.columns):
    party_votes = df.groupby("Party", dropna=False)["Votes"].sum().sort_values(ascending=False)
    party_votes.plot(kind="bar", figsize=(12, 6))
    plt.title("Total Votes by Political Party")
    plt.xlabel("Political Party")
    plt.ylabel("Votes")
    plt.tight_layout()
    plt.show()
else:
    print("Update the column names to match the dataset.")
```

## Power BI Dashboard

1. Open Power BI Desktop.
2. Select **Home → Get Data → Text/CSV**.
3. Import the election-results CSV.
4. Check data types and clean columns in Power Query if needed.
5. Create visuals that match the available fields, such as party-wise votes, seats won, constituency results, and candidate vote counts.
6. Add slicers for party and constituency where supported by the dataset.
7. Save the report as a `.pbix` file.

## Tableau Dashboard

1. Open Tableau.
2. Connect to the election-results CSV.
3. Verify data types and field names.
4. Build charts for party performance and constituency-level results.
5. Add filters for party and constituency when the relevant fields are available.
6. Save the workbook as a `.twb` or `.twbx` file.

## Validation and Responsible Reporting

- Cross-check totals and winners against an official election-results source.
- Clearly identify the source and date of the downloaded dataset.
- Distinguish **seats won**, **votes received**, and **vote share**; they measure different things.
- Do not report a winner, vote count, or margin unless the dataset supports it.
- If the dataset contains only partial or sample records, label the analysis accordingly.

## Expected Outcome

The project provides a reproducible workflow for cleaning election data, exploring party and constituency performance, and presenting the results through Python visualizations and interactive Power BI and Tableau dashboards.

## Author

- **Student:** [Your Name]
- **Register Number:** [Your Register Number]
- **Course:** Framework for Data Visual Analytics (FDVA)
- **Project:** Tamil Nadu 2026 Election Result Analysis

## License

For academic use. Include the dataset's original attribution and follow its license or terms of use.
