# Flu Vaccination Provider Location Analysis

Investigating the relationship between flu vaccine provider density and vaccination rates across U.S. states and counties. 

Data was taken from two CDC API's, one containing information about vaccine distribution centers, and the other containing information about vaccination rate accross various geographic and demographic groups.

## Key Findings

- No meaningful relationship between provider density and vaccination rates at both state and county levels
- Finding is consistent across all demographic groups represented in data (age, race, risk categories)
- Provider characteristics (hours, insurance acceptance) were not predictive of vaccination rates
- Policy implication: Simply increasing vaccination sites at the state or county level is unlikely to improve vaccination rate for those geographies. 

## Background

The CDC publishes weekly flu vaccination rates for every state and many counties, alongside a comprehensive database of ~202k flu vaccine providers nationwide that was upkept until 2024. 
The main research question is whether or not areas with more vaccination sites will havea increased vaccination rates, and if so, how does this difference appear in different demographic groups.
The purpose of thise questioning is to determine whether or not increasing the number of vaccination cites is an effective way of increasing seasonal flu vaccination rate, or whether other efforts such as 
public health awareness campaigns, science education, or more targetted approaches would be useful. 

**Research Question**: Does vaccination site density at the state or county level correlate with higher flu vaccination coverage for those areas. 

## Data Sources

- **CDC Flu Vaccinating Provider Locations** (July 2024): 202k provider records
  - API: https://data.cdc.gov/Flu-Vaccinations/Vaccines-gov-Flu-vaccinating-provider-locations/bugr-bbfr/about_data
- **CDC Influenza Vaccination Coverage** (Jan 2025): 220k coverage records  
  - API: https://data.cdc.gov/Flu-Vaccinations/Influenza-Vaccination-Coverage-for-All-Ages-6-Mont/vh55-3he6/about_data
- **US Census Data (2022 ACS 5-year)**: County population estimates via `censusdata` library

## Methodology

1. **Data Collection**: Retrieved datasets via CDC Socrata API
2. **Data Processing**: 
   - Filtered coverage data to 2023-2024 season, month 12 (annual totals)
   - Mapped provider ZIP codes to counties for geographic aggregation
   - Calculated vaccination rates by state and county
3. **Feature Engineering**: Created "providers per 1,000 people" metric using Census population data
4. **Statistical Analysis**: Pearson correlations between provider density and vaccination rates
5. **Robustness Testing**: Analyzed across multiple demographic breakdowns (age groups, race/ethnicity, risk categories)

## Results & Analysis

*[You'll add your key visualizations here - scatter plots, correlation matrices, etc.]*

### State-Level Analysis
- Sample: 50 states + DC
- Correlation: -0.2841
- P-value: 0.045585
- Effect size: 8.1%

### County-Level Analysis  
- Sample: 1369 counties with complete data
- Correlation: 0.017
- P-value: 0.5179
- Effect size: 0.02%

### Demographic Subgroup Analysis
Tested 18 different population segments:
- Mean correlation: -0.319
- Range: -0.3499 to -0.0808

## Conclusions & Recommendations

**For Public Health Policy:**
- **Avoid supply-side interventions**: Adding more vaccination sites is unlikely to increase uptake
- **Focus on demand-side strategies**: Address vaccine hesitancy, awareness, and convenience barriers
- **Resource allocation**: Redirect resources from site expansion to education and outreach programs

**For Healthcare Systems:**
- Optimize existing site utilization rather than expanding locations
- Investigate other factors driving vaccination rates (accessibility, trust, messaging)

## Technical Details

### Requirements
```
pandas>=1.5.0
numpy>=1.24.0
matplotlib>=3.7.0
seaborn>=0.12.0
scipy>=1.10.0
requests>=2.28.0
censusdata>=1.15.0
```

### Running the Analysis
1. Clone this repository
2. Install requirements: `pip install -r requirements.txt`
3. Extract data files: `unzip data/processed_data.zip -d data/`
4. Run notebooks in order:
   - `01_data_scraping.ipynb` - Data collection from CDC APIs
   - `02_data_cleaning.ipynb` - Data processing and feature engineering  
   - `03_analysis.ipynb` - Statistical analysis and visualizations

### Project Structure
```
├── notebooks/          # Analysis notebooks
├── data/
│   ├── raw/           # Original datasets
│   └── processed/     # Cleaned data (zipped)
├── visualizations/    # Key plots
└── README.md
```
