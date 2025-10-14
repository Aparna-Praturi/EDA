#  EduScope — Global Education Insights 
A comprehensive analysis of global education data to identify key trends, disparities, and potential areas for improvement in educational systems worldwide. 

**Exploratory Data Analysis on World Bank Education Statistics (1960–2022)**  

The project combines **multi-decade data cleaning**, **correlation-based feature reduction**, and **cross-regional analysis** to identify patterns in enrollment, teacher availability, and learning outcomes worldwide.  
Insights are visualized interactively through a **Power BI dashboard** for region-wise comparison.

---

##  About

**EduScope** is a data-driven analysis of how education systems have evolved globally over time.  
Built using **Python (Pandas, Seaborn)** and **Power BI**, it focuses on:  
- Identifying **key indicators** of educational access and quality,  
- Comparing trends across **countries and World Bank regions**, and  
- Revealing correlations between **economic context** (GDP, unemployment) and **learning outcomes** (enrollment, survival rates).  

This project translates large-scale World Bank data (1960–2022) into **interpretable insights** on the state of primary education around the world.

---

##  Data Source  

- **Source:** [World Bank Open Data — Education Statistics (EdStats Series)](https://data.worldbank.org)  
- **Files Used:**  
  - `EdStatsCountry-Series.csv`  
  - `EdStatsCountry.csv`  
  - `EdStatsData.csv`  
  - `EdStatsFootNote.csv`  
  - `EdStatsSeries.csv`  

### Dataset Overview
- **Time coverage:** 1960 – 2022  
- **Years analyzed in notebook:** 1990, 1995, 2000, 2005, 2010  
- **Granularity:** Country-level data, aggregated to World Bank regions  
- **Structure:**  
  - ~244 columns (4 identifier columns + ~240 yearly values)  
  - 4 identifiers: `Country Name`, `Country Code`, `Indicator Name`, `Indicator Code`  
  - Each remaining column corresponds to a **year-specific value** for an indicator  

---

##  Analytical Workflow (Notebook)

All analysis steps are implemented in `EDA_World_Education_Data.ipynb`.

### 1. Data Loading
The notebook loads all five EdStats files to construct a unified dataset:
```python
df1 = pd.read_csv('EdStatsCountry-Series.csv')
df2 = pd.read_csv('EdStatsCountry.csv')
df3 = pd.read_csv('EdStatsData.csv')
df4 = pd.read_csv('EdStatsFootNote.csv')
df5 = pd.read_csv('EdStatsSeries.csv')
```

df_country → country-level metadata (region, income group)

df_edstats → main education indicators by year

df_edstats_countries_* and df_edstats_groups_* → filtered subsets for selected years

### 2. Data Cleaning

- Removed rows missing essential geographic info (e.g., Region, Income Group)

- Filtered to retain primary education–related indicators

- Handled missing numerical values using median or forward-fill imputation

- Renamed and standardized indicator names for clarity

### 3.Feature Exploration

- The full dataset initially contained 60+ primary education indicators.

- Distribution analysis and summary statistics were used to examine outliers and sparsity.

- The time coverage extended back to 1960, but early years had significant missingness.
  
- For consistency and coverage, analysis focused on the subset of 1990 – 2010.

### 4.Correlation-Based Feature Reduction

- Feature reduction was manual and correlation-based — not algorithmic.

Steps:

- Generated a correlation matrix among education indicators

- Identified pairs with |r| > 0.9 (strongly correlated variables)

- Removed redundant or overlapping features

- Retained a compact, interpretable feature set emphasizing education access, outcomes, and economic context

Final selected indicators:

- Net enrolment rate (male/female)

- Survival rate to end of primary (male/female)

- Pupil–teacher ratio

- % of female teachers

- GDP per capita

- Unemployment rate

- Official entrance age to school

### 5. Regional Aggregation

- Grouped countries by World Bank region

- Computed regional averages for key years (1990–2010)

- Produced a region-level dataset used as input to the Power BI dashboard

6️⃣ Exploratory Data Analysis

- Compared gender differences in enrollment and survival rates

- Analyzed regional disparities in teacher availability and student outcomes

- Examined economic associations (e.g., GDP vs. survival rates)

Produced multiple visualizations:

- Correlation heatmaps

- Regional comparison bar charts

- Scatter plots of GDP vs. pupil–teacher ratio

- Temporal trends in enrollment and survival rates

## Power BI Dashboard

The Power BI dashboard summarizes these results interactively.

### Features:

- Filters for 7 World Bank regions

- KPIs: Population, GDP per capita, unemployment rate

Trend lines for Net Enrollment Rate (1990–2010)

- Gender-wise survival rate gauges

- Regional Pupil–Teacher Ratio comparisons

- Bubble chart: Female Teacher % vs. Survival Rate (bubble size = GDP)

##  Tools & Technologies
| **Task** | **Tools / Libraries** |
|-----------|-----------------------|
| Data Source | World Bank Open Data (EdStats Series) |
| Data Processing | Python, Pandas, NumPy |
| Visualization (EDA) | Matplotlib, Seaborn |
| Dashboard | Power BI |
| Environment | Jupyter Notebook |

                     


## Key Findings

- Years analyzed: 1990 – 2010 (selected for completeness)

- GDP per capita shows strong correlation with primary survival rate.

- Higher female teacher percentages are associated with better student survival.

- Sub-Saharan Africa and South Asia display the highest pupil–teacher ratios.

- Gender enrollment gaps narrowed significantly from 1990 to 2010.

- Official school entrance age varies between 5 – 7 years globally.
