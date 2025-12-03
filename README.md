# Unemployment & Voter Turnout Analysis
## Statistical Analysis Project - STA 702

**Research Question:** How does local economic downturn relate to voter turnout in U.S. elections at the county level?

This project analyzes the relationship between county-level unemployment rates and voter turnout across U.S. presidential and midterm elections (2004-2022), with emphasis on heterogeneous effects across urban/rural counties.

## 📁 Project Structure

```
├── data/
│   ├── raw/                          # Original datasets (Git LFS)
│   │   ├── ICPSR_38506-V2.zip       # Voting data (ICPSR)
│   │   └── la.data.64.County.txt    # Unemployment data (BLS)
│   ├── processed/                    # Clean, analysis-ready datasets
│   │   ├── merged_voting_unemployment_complete.csv  # ⭐ PRIMARY DATASET
│   │   ├── voting_population_cleaned.csv           # Cleaned voting data
│   │   ├── unemployment_county_year.csv            # Cleaned unemployment data
│   │   └── analysis_data_r.csv                     # R analysis dataset (with derived vars)
│   └── output/                       # Regression results
│       ├── regression_models.RData   # Saved R model objects
│       └── regression_table.tex      # Publication-ready table
├── notebooks/                        # Analysis code
│   ├── Research_Question_1_Analysis.qmd   # ⭐ MAIN ANALYSIS (R/Quarto)
│   ├── Preprocess_VotingPop.ipynb         # ⭐ DATA PREP (clean + merge + QA)
│   ├── unemployment_preprocessing.R       # Unemployment data cleaning
│   └── Project_Proposal.qmd               # Original proposal
├── plots/                            # Visualizations
└── economic_factors/                 # Census economic data
```

## ✅ Project Status

### Completed
- ✅ **Data Collection & Cleaning** (Voting + Unemployment data)
- ✅ **Data Quality Assessment** (Comprehensive diagnostics)
- ✅ **Data Merging** (30,912 county-year observations, 2004-2022)
- ✅ **Exploratory Analysis** (Descriptive stats, visualizations)
- ✅ **Statistical Modeling** (5 regression models with interaction terms)
- ✅ **Results Documentation** (Quarto report ready)

### Key Deliverables
- **Data Preprocessing:** `Preprocess_VotingPop.ipynb` (all cleaning, QA, merging)
- **Primary Analysis:** `Research_Question_1_Analysis.qmd` (render to HTML/PDF)
- **Clean Dataset:** `merged_voting_unemployment_complete.csv` (30,912 obs)
- **Regression Results:** Saved in `data/output/regression_models.RData`

## 🔍 Key Findings

### 1. Unemployment-Turnout Relationship
- **Weak negative correlation** (r = -0.041, p < 0.001) between unemployment and voter turnout
- Correlation is **stronger in midterm elections** (r = -0.135) than presidential elections (r = -0.083)
- **State-level correlation** is stronger (r = -0.309) than county-level

### 2. Election Type Dominates
- **Presidential elections:** 58.8% average turnout
- **Midterm elections:** 42.6% average turnout  
- **16.3 percentage point difference** (t = 94.1, p < 0.001) - highly significant

### 3. Temporal Patterns
- **2010 unemployment peak** (9.29%) during Great Recession aftermath
- **2020 turnout peak** (62.9%) despite COVID-19 pandemic
- **2022 lowest unemployment** (3.60%) in the analysis period

### 4. Geographic Variation
- **Highest turnout states:** Maine (66.0%), Colorado (65.3%), Montana (63.0%)
- **Lowest turnout states:** West Virginia (35.5%), Tennessee (39.6%), Mississippi (41.6%)
- **3,007 counties** have complete data for all 10 election cycles (balanced panel)

## Data Quality Notes

### Missing Data Patterns
- **Years 2000-2002:** 100% missing CVAP (Citizen Voting Age Population) - excluded from analysis
- **Years 2004-2022:** <1% missing CVAP, suitable for modeling
- **Senate elections:** ~53% missing (expected - not all years have Senate races)
- **Presidential elections:** ~47% missing (expected - presidential races every 4 years)

### FIPS Code Issues
- **99.7% match rate** between voting and unemployment data
- **11 unmatched counties:** Primarily Connecticut (different coding system) and reorganized counties
- Unmatched details documented in `Preprocess_VotingPop.ipynb`

### Negative Values in Voter Turnout
- **North Dakota (State FIPS 38):** 477 rows with `-1.0` (no voter registration requirement)
- **6 records** with negative turnout (data errors) - flagged for exclusion
- **Other States:** Illinois, South Carolina, Mississippi contain some `-1.0` values (missing data indicators)
- **Recommendation:** Filter out these values or treat them as `NaN` during analysis.

## 🚀 Quick Start

### To Reproduce Analysis
1. **Open main analysis:** `notebooks/Research_Question_1_Analysis.qmd`
2. **Render in RStudio:** Click "Render" or press `Ctrl+Shift+K`
3. **View results:** Opens as HTML with all analysis, plots, and regression tables

### To Explore Data
- **Dataset:** `data/processed/merged_voting_unemployment_complete.csv`
- **Data quality report:** See `Preprocess_VotingPop.ipynb` for full diagnostics
- **Visualizations:** `plots/` directory

### Dataset Details
- **30,912 observations** (county-year level)
- **3,103 counties** across 50 states
- **10 election cycles** (2004-2022: 5 presidential + 5 midterm)
- **Complete data** (no missing values in key variables)
- **Balanced panel** available (3,007 counties with all 10 years)

### County Classification
Counties classified by **CVAP (Citizen Voting Age Population)**:
- **Urban**: CVAP > 50,000 (large metropolitan counties)
- **Suburban**: CVAP 10,000-50,000 (medium-sized counties)
- **Rural**: CVAP < 10,000 (small, sparsely populated counties)

This classification captures heterogeneous effects of unemployment across different county contexts.

## 📊 Main Results

**Research Question:** How does local economic downturn relate to voter turnout?

### Regression Results Summary (5 Models)

| Model | Unemployment Coef | R² | Interpretation |
|-------|-------------------|-----|----------------|
| Simple OLS | -0.003*** | 0.002 | Baseline: weak negative effect |
| + Election Type | -0.006*** | 0.232 | Presidential elections +16.7% turnout |
| + Interaction | -0.010*** (rural) | 0.254 | **Stronger effect in rural counties** |
| Two-Way FE | -0.001 | 0.570 | Within-county: no significant effect |
| FE + Interaction | -0.003*** | 0.571 | Effect persists with controls |

**Key Finding:** Unemployment has a **small negative effect** on turnout (-0.3 to -0.6 percentage points per 1% unemployment increase), **strongest in rural counties**, but election type matters far more (16.7% difference between presidential and midterm elections).

## 📚 Data Sources & Citations

**Voting Data:**
> Clary, Will, et al. National Neighborhood Data Archive (NaNDA): Voter Registration, Turnout, and Partisanship by County, United States, 2004-2022 (ICPSR 38506). Ann Arbor, MI: Inter-university Consortium for Political and Social Research, 2024. https://doi.org/10.3886/ICPSR38506.v2

**Unemployment Data:**
> Bureau of Labor Statistics, Local Area Unemployment Statistics (LAUS), 1990-2024.

## 👥 Team
Diwas Puri, Xinhao Zhang, Tea Tafaj, Tony Ngari - STA 702, Duke University