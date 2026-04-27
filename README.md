Aim: To perform extensive data cleaning, exploratory data analysis (EDA), and geospatial visualization on the global COVID-19 dataset using Python.

1. Theory

Exploratory Data Analysis (EDA) is an approach to analyzing data sets to summarize their main characteristics, often with visual methods. In the context of the COVID-19 pandemic, EDA helps in understanding the trajectory of the virus, identifying hotspots, and evaluating recovery rates across different geographical regions.

<img width="1808" height="543" alt="image" src="https://github.com/user-attachments/assets/61ebb026-a0d5-4134-92c0-0a7b8c8a1d1d" />

Key Metrics Used:

Confirmed Cases: Total number of people infected.

Deaths: Total number of fatalities.

Recovered: Total number of people who survived the infection.

Active Cases: Calculated as Active=Confirmed−(Deaths+Recovered). This represents the current burden on the healthcare system.

2. Algorithm & Workflow

The experiment followed a structured data science pipeline:

Data Ingestion: Loading the raw CSV file containing global daily reports.

Data Cleaning & Preprocessing:

Dropping unnecessary columns like SNo and Last Update.

Data Acquisition: Import the dataset using pd.read_csv().

Structural Optimization: * Remove non-informative columns using .drop().

Inspect the data architecture using .info() to identify data type mismatches.

Data Type Normalization:

Convert the ObservationDate from a string to a datetime64 object to enable time-series slicing.

Convert floating-point counts (like 1.0, 2.0) into int64 to save memory and ensure proper mathematical representation.

Handling Nulls: Use .fillna(0) for numerical counts and .fillna("Unknown") for categorical labels to prevent errors during aggregation.

Snapshot Analysis:

Use .max() to find the most recent date in the record.

Filter the DataFrame to create a latest_data subset, representing the current global status.

Statistical Aggregation:

Group by Country/Region to get national totals.

Group by Province/State for localized analysis (specifically for India).

Visualization:

Plot global confirmed and recovered cases using px.choropleth.

Sort and slice the data using sort_values().head(20) to find the most impacted regions.

pd.to_datetime() : Standardizes date formats for time-series analysis.

px.choropleth() : Creates interactive world maps.

5. Conclusion

This experiment successfully demonstrates the power of Python for handling large-scale datasets (300,000+ rows). By cleaning the data and standardizing types, we were able to transform raw observational logs into actionable insights.

Geospatial visualization provided a clear picture of the pandemic's global footprint, while Feature Engineering (Active cases) allowed for a deeper understanding of the pandemic beyond just cumulative totals. The analysis concludes that while total confirmed cases provide the scale of the pandemic, active case counts and recovery rates are more indicative of the current healthcare status of a region.
