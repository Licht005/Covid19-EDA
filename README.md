# Covid19-EDA
# **Exploratory Data Analysis on COVID-19 Dataset**

## **Overview**
This analysis focuses on understanding the COVID-19 dataset, which contains information about confirmed cases, deaths, recoveries, active cases, and WHO regions across different countries and over time. The dataset spans from January 2020 to July 2020 and includes a total of 49,068 entries with 10 columns.

---

## **Steps Performed**

### 1. **Initial Data Exploration**
- **Dataset Structure**:
  - Rows: 49,068
  - Columns: 10 (including Province/State, Country/Region, Lat, Long, Date, Confirmed, Deaths, Recovered, Active, and WHO Region)
- **Missing Data**:
  - The column **Province/State** had 34,404 missing values.
  - All other columns were complete with no missing values.

### 2. **Data Cleaning**
- **Province/State Column Dropped**:
  - As it contained significant missing data and wasn't critical for the analysis, this column was removed to simplify the dataset.
- Remaining columns were retained for further analysis.

### 3. **Exploratory Analysis**
- **Trends Over Time**:
  - Plotted the number of confirmed cases, deaths, recoveries, and active cases over time to understand trends.
  - Observed that July 27, 2020, marked the peak in confirmed cases, deaths, and recoveries.

- **Correlation Analysis**:
  - Examined correlations among numerical variables using a heatmap.
  - Key relationships:
    - Confirmed cases were strongly positively correlated with deaths and recoveries.
    - Active cases had weaker correlations with deaths and recoveries.
    - Latitude and Longitude showed no significant correlations with other metrics.

- **Minimum and Maximum Cases**:
  - Identified the dates of minimum and maximum values for confirmed cases, deaths, recoveries, and active cases:
    - **Maximum Confirmed Cases**: July 27, 2020
    - **Minimum Active Cases**: June 2, 2020

### 4. **Country-Level Analysis**
- Aggregated the data by `Country/Region` to analyze total cases, deaths, recoveries, and active cases for each country.
- Ghana-specific insights:
  - Ghana was found in the dataset with the following statistics:
    - Total Confirmed Cases: _(Calculated during the analysis)_
    - Total Recoveries: _(Calculated during the analysis)_
- Identified the countries with the most and least cases, deaths, recoveries, and active cases:
  - Most Confirmed Cases: United States
  - Most Deaths: United States
  - Least Confirmed Cases: Tokelau (Zero cases)
  - Least Deaths: Tokelau (Zero deaths)

---

## **README**

### **Dataset Description**
The dataset contains global COVID-19 data with the following key columns:
- **Date**: The date of the record.
- **Country/Region**: The country or region where the data was recorded.
- **Lat and Long**: Latitude and longitude of the location.
- **Confirmed**: Cumulative confirmed COVID-19 cases.
- **Deaths**: Cumulative deaths due to COVID-19.
- **Recovered**: Cumulative recovered cases.
- **Active**: Current active cases.
- **WHO Region**: The World Health Organization region.

### **Prerequisites**
- Python (version 3.6 or above)
- Libraries used: `pandas`, `numpy`, `matplotlib`, `seaborn`

### **Steps to Reproduce the Analysis**
1. **Load the Dataset**:
   ```python
   import pandas as pd
   df = pd.read_csv("path_to_dataset.csv")
   ```
2. **Clean the Data**:
   - Drop the **Province/State** column.
     ```python
     df.drop(columns=['Province/State'], inplace=True)
     ```
3. **Perform Visualizations**:
   - Plot trends over time:
     ```python
     df.groupby('Date')[['Deaths', 'Recovered', 'Active']].sum().plot(figsize=(10, 6))
     ```
   - Correlation heatmap:
     ```python
     import seaborn as sns
     sns.heatmap(df.corr(), annot=True, cmap='coolwarm')
     ```
4. **Analyze Country-Level Data**:
   - Group by `Country/Region`:
     ```python
     country_data = df.groupby('Country/Region').agg({
         'Confirmed': 'sum',
         'Deaths': 'sum',
         'Recovered': 'sum',
         'Active': 'sum'
     }).reset_index()
     ```
   - Find totals for Ghana:
     ```python
     ghana_data = df[df['Country/Region'] == 'Ghana']
     total_confirmed = ghana_data['Confirmed'].sum()
     total_recovered = ghana_data['Recovered'].sum()
     ```

---

### **Key Findings**
- Significant missing data in the **Province/State** column was addressed by removing it.
- Peak case numbers aligned with July 2020, reflecting the global trend.
- Strong correlations were observed between confirmed cases, deaths, and recoveries.
- Ghana's total confirmed cases and recoveries were successfully extracted.
- Insights at the country level revealed major disparities in the impact of COVID-19 between regions.

### **Conclusion**
This analysis provides a comprehensive understanding of the COVID-19 dataset, highlighting key trends and patterns globally and for specific countries like Ghana. The approach can be extended to predict trends, assess the effectiveness of interventions, and guide policy decisions.

---
