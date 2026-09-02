# Employee Data Analysis & Cleaning Project

## Project Overview
This project demonstrates an end-to-end data cleaning and exploratory data analysis (EDA) workflow using Python, Pandas, NumPy, Matplotlib, and Seaborn.

The project uses an intentionally **unclean employee dataset** containing missing values, duplicates, inconsistent categories, invalid ages, negative salaries, inconsistent dates, and invalid email addresses.

## Dataset
**Raw file:** `unclean_employee_data_analysis_project.csv`

### Columns
| Column | Description |
|---|---|
| Employee_ID | Unique employee identifier |
| Name | Employee name |
| Age | Employee age |
| Gender | Employee gender |
| Department | Employee department |
| Job_Role | Employee job role |
| Salary | Employee salary |
| Joining_Date | Employee joining date |
| City | Employee city |
| Email | Employee email address |
| Experience_Years | Years of professional experience |
| Performance_Score | Employee performance category |

## Data Quality Problems
- Missing values
- Duplicate records
- Invalid and unrealistic ages
- Negative salary values
- Salary values containing text
- Inconsistent department and city names
- Extra spaces
- Inconsistent gender values
- Invalid email addresses
- Invalid/mixed date formats
- Incorrect data types

## Project Objectives
1. Load and understand the raw dataset.
2. Inspect rows, columns, data types, and statistics.
3. Identify and handle missing values.
4. Detect and remove duplicates.
5. Clean inconsistent text categories.
6. Convert columns to appropriate data types.
7. Handle invalid age and salary values.
8. Convert joining dates to datetime.
9. Validate email values.
10. Perform exploratory data analysis.
11. Create visualizations.
12. Generate business insights.
13. Export the cleaned dataset.

## Project Workflow
```text
Raw Dataset
    ↓
Data Loading
    ↓
Data Understanding
    ↓
Data Quality Check
    ↓
Data Cleaning
    ↓
Exploratory Data Analysis
    ↓
Visualization
    ↓
Business Insights
    ↓
Clean Dataset
```

## Technologies Used
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

## Important Cleaning Examples

### Check Missing Values
```python
df.isnull().sum()
```

### Check Duplicates
```python
df.duplicated().sum()
```

### Remove Duplicates
```python
df = df.drop_duplicates()
```

### Clean Department
```python
df["department"] = df["department"].str.strip().str.lower()

df["department"] = df["department"].replace({
    "it": "IT",
    "finance": "Finance",
    "h.r": "HR",
    "human resources": "HR",
    "sales": "Sales",
    "marketing": "Marketing",
    "operations": "Operations"
})
```

### Clean Salary
```python
df["salary"] = (
    df["salary"]
    .astype(str)
    .str.replace(",", "", regex=False)
    .str.replace(" INR", "", regex=False)
)

df["salary"] = pd.to_numeric(df["salary"], errors="coerce")

df.loc[df["salary"] < 0, "salary"] = np.nan
```

### Clean Age
```python
df["age"] = pd.to_numeric(df["age"], errors="coerce")

df.loc[(df["age"] < 18) | (df["age"] > 65), "age"] = np.nan

df["age"] = df["age"].fillna(df["age"].median())
df["age"] = df["age"].astype(int)
```

### Convert Date
```python
df["joining_date"] = pd.to_datetime(
    df["joining_date"],
    errors="coerce"
)
```

## Exploratory Data Analysis Questions
- What is the total number of employees?
- What is the average salary?
- Which department has the highest average salary?
- Which department has the most employees?
- Which city has the most employees?
- What is the average employee age?
- Which job role has the highest salary?
- Does experience relate to salary?
- Which performance category is most common?

## Example Analysis
```python
# Employees by department
df["department"].value_counts()

# Average salary by department
df.groupby("department")["salary"].mean().sort_values(ascending=False)

# Employees by city
df["city"].value_counts()

# Average salary by job role
df.groupby("job_role")["salary"].mean().sort_values(ascending=False)
```

## Recommended Visualizations
- Salary distribution
- Employees by department
- Average salary by department
- Age distribution
- Experience vs salary

## Project Structure
```text
Employee_Data_Analysis/
│
├── data/
│   ├── unclean_employee_data_analysis_project.csv
│   └── clean_employee_data.csv
│
├── notebook/
│   └── employee_data_analysis.ipynb
│
├── visualizations/
│   ├── salary_by_department.png
│   ├── employees_by_city.png
│   ├── age_distribution.png
│   └── experience_vs_salary.png
│
├── README.md
└── requirements.txt
```

## Learning Outcomes
- Python programming
- Pandas data manipulation
- NumPy
- Data cleaning
- Missing-value handling
- Duplicate detection
- Data-type conversion
- String cleaning
- Invalid-value handling
- Exploratory Data Analysis
- Data visualization
- Business insight generation
- GitHub project documentation

## Conclusion
This project demonstrates how an unclean real-world-style employee dataset can be transformed into an analysis-ready dataset. It covers data loading, cleaning, exploratory analysis, visualization, and business insights.

## Author
**Vignesh**

**Tools:** Python | Pandas | NumPy | Matplotlib | Seaborn | Jupyter Notebook
