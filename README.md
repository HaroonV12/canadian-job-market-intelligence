# Canadian Job Market Intelligence

A data analytics and machine-learning project examining Canadian hiring demand, advertised salaries, employment conditions, and occupational patterns using January 2025 Job Bank postings.

## Project Overview

This project analyzes 101,570 job postings advertised on Canada’s National Job Bank. It combines data cleaning, exploratory analysis, salary prediction, and occupation clustering to identify patterns in the Canadian labour market.

The project addresses the following questions:

* Which provinces and occupations have the greatest hiring demand?
* Which occupations advertise the highest salaries?
* How transparent are employers about salary, education, and experience requirements?
* What characteristics help predict an advertised salary?
* Can occupations be grouped according to demand, salary, and salary transparency?
* What does the dataset suggest about analytics and AI-related employment?

## Dataset

The data comes from the Government of Canada’s [Job Postings Advertised on Canada’s National Job Bank](https://open.canada.ca/data/en/dataset/ea639e28-c0fc-48bf-b5dd-b8899bd43072) dataset.

This analysis uses the January 2025 English dataset.

The original data file is not included in this repository because of its size. To reproduce the project, download the data and place it at:

```text
data/raw/job_bank_jan_2025.csv
```

## Key Findings

### Hiring Demand

The occupations with the greatest numbers of advertised vacancies included:

* Retail salespersons and visual merchandisers — 6,688 vacancies
* Cooks — 5,161 vacancies
* Food-service supervisors — 5,112 vacancies
* Transport truck drivers — 4,671 vacancies
* Food-counter attendants and kitchen helpers — 4,020 vacancies

Ontario had the largest number of postings and advertised vacancies, followed by Québec, British Columbia, and Alberta.

### Advertised Salaries

Approximately 52.1% of postings contained salary information that passed the project’s validity checks.

Among valid salary postings:

* Median hourly salary: $25.53
* Mean hourly salary: $29.18
* Lower quartile: $20.00
* Upper quartile: $34.10
* 90th percentile: $42.50

British Columbia had a median advertised salary of $28.00 per hour, compared with $26.50 in Ontario and $25.00 in both Québec and Alberta.

Some of the highest-paying occupations included medical specialists, general practitioners, dentists, psychologists, nurse practitioners, and pharmacists. Small occupational samples were excluded from salary rankings.

### Salary Prediction

Three prediction approaches were evaluated:

* Median baseline
* Multiple linear regression
* K-nearest neighbours regression

The full-data linear-regression model achieved:

* MAE: $5.51 per hour
* RMSE: $9.83 per hour
* R²: 0.584

On a common 8,000-posting sample, the tuned KNN model achieved an MAE of $5.72, compared with $6.21 for linear regression and $8.85 for the median baseline.

The selected KNN model used 30 neighbours with distance-based weighting. Occupation group was its most influential feature, followed by province or territory.

Prediction errors were greatest among highly paid positions, where the models tended to underestimate advertised salaries.

### Occupation Clustering

K-means clustering grouped 335 occupations into three categories:

1. **Moderate demand, strong salary coverage**
   187 occupations with an average median salary of $28.50 and salary coverage of 76.5%.

2. **Higher salary, limited salary coverage**
   134 occupations with an average median salary of $39.20 but salary coverage of only 34.7%.

3. **Very high demand, lower salary**
   14 occupations with an average of 3,287 advertised vacancies and an average median salary of $22.80.

The clustering results suggest that occupations with the greatest hiring demand do not necessarily advertise the highest salaries.

### Analytics and AI Market

A keyword-based analysis identified approximately 618 analytics and AI-related postings across nine provinces and territories.

These postings had a median advertised salary of approximately $42 per hour. Toronto had the largest number of identified postings, followed by Montréal.

Because this subset was identified through job-title keywords, it may exclude relevant positions or include positions that only partially involve analytics or AI.

## Project Structure

```text
canadian-job-market-intelligence/
│
├── data/
│   ├── raw/
│   └── processed/
│
├── notebooks/
│   ├── 01_data_inspection.ipynb
│   ├── 02_exploratory_analysis.ipynb
│   ├── 03_salary_prediction.ipynb
│   └── 04_occupation_clustering.ipynb
│
├── reports/
│   ├── figures/
│   ├── occupation_clusters.csv
│   └── salary_model_comparison.csv
│
├── .gitignore
├── LICENSE
├── README.md
└── requirements.txt
```

## Notebook Workflow

### `01_data_inspection.ipynb`

* Loads and inspects the original dataset
* Standardizes column names
* Checks missing values and duplicate records
* Converts date columns
* Normalizes salaries to estimated hourly values
* Applies salary-validity checks
* Saves the cleaned dataset as Parquet

### `02_exploratory_analysis.ipynb`

* Analyzes hiring demand by province and occupation
* Compares advertised salary patterns
* Examines salary transparency
* Evaluates employment types and qualification requirements
* Investigates analytics and AI-related postings
* Creates and saves project visualizations

### `03_salary_prediction.ipynb`

* Creates a baseline salary model
* Trains a multiple linear-regression model
* Tunes a K-nearest neighbours model
* Compares MAE, RMSE, and R²
* Examines prediction errors
* Evaluates feature importance

### `04_occupation_clustering.ipynb`

* Creates an occupation-level dataset
* Standardizes clustering features
* Uses the elbow method to select the number of clusters
* Applies K-means clustering
* Profiles and interprets the resulting occupation groups

## Tools Used

* Python
* pandas
* NumPy
* Matplotlib
* seaborn
* scikit-learn
* PyArrow
* Jupyter Notebook
* Visual Studio Code
* Git and GitHub

## Running the Project

1. Download or clone the repository.
2. Create a Python virtual environment.
3. Install the required packages:

```bash
pip install -r requirements.txt
```

4. Download the January 2025 Job Bank dataset and save it as:

```text
data/raw/job_bank_jan_2025.csv
```

5. Run the notebooks in order:

```text
01_data_inspection.ipynb
02_exploratory_analysis.ipynb
03_salary_prediction.ipynb
04_occupation_clustering.ipynb
```

The first notebook creates the processed Parquet file required by the remaining notebooks.

## Limitations

* The dataset represents postings advertised on Job Bank and not every Canadian job vacancy.
* The analysis covers January 2025 and should not be interpreted as a long-term labour-market trend.
* Approximately half of the postings lacked usable salary information.
* Salary normalization uses standard working-period assumptions.
* Predicted salaries are estimates and should not be used as individual compensation recommendations.
* Analytics and AI postings were identified through keywords rather than manual classification.
* K-means cluster names are descriptive interpretations and not official Job Bank categories.

## License

See the `LICENSE` file for licensing information.
