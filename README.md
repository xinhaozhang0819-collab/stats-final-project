# Unemployment & Voter Turnout Analysis
## Statistical Analysis Project - STA 702

**Research Question:** How does local economic downturn relate to voter turnout in U.S. elections at the county level?

This project analyzes the relationship between county-level unemployment rates and voter turnout across U.S. presidential and midterm elections (2004-2022), with emphasis on heterogeneous effects across urban, suburban, and rural counties.

## 📁 Project Structure

```
├── data/
│   ├── raw/                          # Original datasets (Git LFS)
│   │   ├── ICPSR_38506-V2.zip        # Voting data (ICPSR)
│   │   └── la.data.64.County.txt     # Unemployment data (BLS)
│   ├── processed/                    # Clean, analysis-ready datasets
│   │   ├── merged_voting_unemployment_complete.csv  # ⭐ PRIMARY DATASET
│   │   ├── voting_population_cleaned.csv            # Cleaned voting data
│   │   ├── unemployment_county_year.csv             # Cleaned unemployment data
│   │   └── analysis_data_r.csv                      # R analysis dataset
│   └── output/                       # Regression results
│       ├── regression_models.RData   # Saved R model objects
│       └── regression_table.tex      # Publication-ready table
├── notebooks/                        # Analysis code
│   ├── RQ1_v2.qmd                    # ⭐ MAIN ANALYSIS (R/Quarto)
│   ├── Preprocess_VotingPop.ipynb    # ⭐ DATA PREP (clean + merge + QA)
│   ├── unemployment_preprocessing.R  # Unemployment data cleaning
│   └── Project_Proposal.qmd          # Original proposal
├── plots/                            # Visualizations
└── economic_factors/                 # Census economic data
```

## ✅ Project Status

### Completed
- ✅ **Data Collection & Cleaning** (Voting + Unemployment data)
- ✅ **Data Quality Assessment** (Comprehensive diagnostics)
- ✅ **Data Merging** (30,912 county-year observations, 2004-2022)
- ✅ **Exploratory Analysis** (Descriptive stats, visualizations)
- ✅ **Statistical Modeling** (Fixed Effects with Interaction Terms)
- ✅ **Results Documentation** (Quarto report finalized)

### Key Deliverables
- **Data Preprocessing:** `Preprocess_VotingPop.ipynb` (all cleaning, QA, merging)
- **Primary Analysis:** `notebooks/RQ1_v2.qmd` (render to HTML/PDF)
- **Clean Dataset:** `merged_voting_unemployment_complete.csv` (30,912 obs)
- **Regression Results:** Saved in `data/output/regression_models.RData`

## 🔍 Key Findings

### 1. Interaction Effects are Significant
- **F-test results** confirm ($p = 0.004$) that the relationship between unemployment and turnout differs significantly across **Rural**, **Suburban**, and **Urban** counties.
- The unemployment effect cannot be treated as uniform across all geographies.

### 2. Modest Substantive Explanatory Power
- While statistically significant, the **economic effect sizes are small**.
- A massive **2 percentage point increase** in unemployment (recession scenario) predicts turnout changes of less than **0.5 percentage points** across all county types.
- **Reference (Rural):** Baseline effect is very small (~0.04 percentage point change per 1% unemployment).
- **Urban/Suburban:** Show slightly larger, positive responsive effects compared to the baseline, but still substantively modest.

### 3. Structural Factors Dominate
- **Election Type** remains the primary driver of turnout (Midterm vs. Presidential gap is ~16 percentage points).
- **State-level variation** accounts for more variance than local economic conditions.

### 4. Interpretation
- Economic stress ("voting with your pocketbook") is **not a dominant mobilizer** for voter turnout at the aggregate county level.
- Local economic conditions play a statistically detectable but practically minor role compared to structural political factors.

## Data Quality Notes

### Missing Data Patterns
- **Years 2000-2002:** 100% missing CVAP (Citizen Voting Age Population) - excluded from analysis
- **Years 2004-2022:** <1% missing CVAP, suitable for modeling
- **Senate elections:** ~53% missing (expected - not all years have Senate races)

### FIPS Code Issues
- **99.7% match rate** between voting and unemployment data
- **11 unmatched counties:** Primarily Connecticut (different coding system) and reorganized counties
- Unmatched details documented in `Preprocess_VotingPop.ipynb`

### Negative Values in Voter Turnout
- **North Dakota (State FIPS 38):** Rows with `-1.0` (no voter registration requirement) were handled.
- **Data cleaning:** Negative values and outliers were filtered out for the final analysis set.

## 🚀 Quick Start

### To Reproduce Analysis
1.  **Open main analysis:** `notebooks/RQ1_v2.qmd`
2.  **Render in RStudio:** Click "Render" or press `Ctrl+Shift+K`
3.  **View results:** Opens as HTML with all analysis, interaction plots, and regression tables

### To Explore Data
- **Dataset:** `data/processed/merged_voting_unemployment_complete.csv`
- **Data quality report:** See `Preprocess_VotingPop.ipynb` for full diagnostics

### Dataset Details
- **30,912 observations** (county-year level)
- **3,103 counties** across 50 states
- **10 election cycles** (2004-2022: 5 presidential + 5 midterm)
- **Balanced panel** availablility

### County Classification
Counties classified by **CVAP (Citizen Voting Age Population)**:
- **Urban**: CVAP > 50,000 (large metropolitan counties)
- **Suburban**: CVAP 10,000-50,000 (medium-sized counties)
- **Rural**: CVAP < 10,000 (small, sparsely populated counties)

This classification captures heterogeneous effects of unemployment across different county contexts.

## 👥 Team
Diwas Puri, Xinhao Zhang, Tea Tafaj, Tony Ngari - STA 702, Duke University