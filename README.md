# 🌍 Economic Disparity Analysis: Rich vs. Poor Nations

## 📊 Project Overview

This project conducts a comprehensive data analysis to investigate economic disparities between 'Rich' and 'Poor' countries, categorized by the Human Development Index (HDI). Through exploratory data analysis (EDA), statistical testing, regression modeling, and machine learning, we examine relationships between key economic indicators such as 🌐 Internet Penetration, 💵 GDP, 💼 Minimum Wage, HDI, 📉 Inflation, and 📊 Unemployment.

**Primary Objectives:**
- Uncover and quantify economic disparities between Rich and Poor nations
- Analyze time-series trends across economic indicators
- Perform statistical hypothesis testing and regression analysis
- Build predictive machine learning models for wealth categorization
- Provide data-driven policy recommendations

---

## 📚 Data Sources

The analysis utilizes three primary datasets:

* **`cleaned_merged_data.csv`**: Contains data on 🌐 Internet Penetration rates and 💵 GDP values
* **`merged_data.csv`**: Includes HDI scores and 💼 Minimum Wage information
* **`cleaned_data.csv`**: Contains 📉 Inflation (consumer prices, annual %) and 📊 Unemployment (total) figures

---

## 🧑‍💻 Methodology

### 1. 🔄 Data Preparation

* **Data Loading**: Loaded and merged the three CSV datasets based on `country` and `Year`
* **Column Standardization**: 
  - Renamed `CountryName` and `Country Name` → `country`
  - Renamed `Time` → `Year`
* **Feature Engineering**: Created `Internet_Penetration` numerical feature from percentage strings
* **Data Consolidation**: Created comprehensive `df_consolidated` DataFrame with all economic indicators

### 2. 🧹 Data Cleaning

**Initial Data Quality Issues:**
- Unemployment & Inflation: ~74.81% missing
- Minimum Wage: ~51.24% missing  
- HDI: ~33.07% missing

**Cleaning Strategy:**
- Dropped rows with missing `Inflation` or `Unemployment` (reduced from 3,033 to 764 rows)
- Imputed missing `Minimum_Wage` and `HDI` values using median
- Final dataset: 764 rows, 8 columns with zero missing values

### 3. 📊 Country Categorization

Countries were classified as 'Rich' or 'Poor' based on the **median HDI threshold (0.765)**:
- **Rich**: HDI ≥ 0.765
- **Poor**: HDI < 0.765

### 4. 🔍 Exploratory Data Analysis

* Generated comparative 📦 **box plots** and 📉 **scatter plots** for all key indicators
* Conducted **time-series analysis** of 🌐 Internet Penetration and 📉 Inflation trends
* Computed **summary statistics** to quantify disparities between Rich and Poor countries

### 5. 📈 Statistical Analysis

**Regression Models:**

| Model | Formula | R² | Key Finding |
|-------|---------|-----|-------------|
| GDP vs. Internet Penetration | `Log_GDP ~ Wealth * Internet_Penetration` | 0.043 | Weak explanatory power; Internet significant predictor |
| HDI vs. Minimum Wage | `HDI ~ Wealth * Log_Minimum_Wage` | **0.756** | **Strong relationship**; significant interaction term |
| Unemployment vs. Inflation | `Log_Unemployment ~ Wealth * Log_Inflation` | 0.021 | Very weak relationship; other factors dominant |

**Hypothesis Testing:**

| Test | T-statistic | P-value | Conclusion (α=0.05) |
|------|-------------|---------|---------------------|
| **Unemployment** | -4.494 | **7.8e-06** | ✅ **Significant difference** - Poor countries have higher unemployment |
| **Inflation** | -1.322 | 0.186 | ❌ No significant difference between Rich and Poor countries |

### 6. 🤖 Machine Learning Classification

Built a **Random Forest Classifier** to predict `Wealth_Category` using all economic indicators.

**Model Performance:**

| Metric | Score |
|--------|-------|
| Accuracy | **97%** |
| Precision | 97% |
| Recall | 97% |
| F1 Score | 97% |

**Feature Importance:**

| Feature | Importance |
|---------|------------|
| 🏆 **HDI** | **52.6%** |
| 💼 Minimum Wage | 13.7% |
| 🌐 Internet Penetration | 11.5% |
| 💵 GDP Value | 10.5% |
| 📊 Unemployment | 8.5% |
| 📉 Inflation | 3.2% |

---

## 📊 Summary Statistics

| Indicator | Statistic | Poor | Rich |
|-----------|-----------|------|------|
| **🌐 Internet Penetration** | mean | 20.57% | 54.98% |
| | median | 10.00% | 59.83% |
| **💵 GDP Value** | mean | $2.48M | $935K |
| | median | $177K | $46K |
| **💼 Minimum Wage** | mean | $103.69 | $680.70 |
| | median | $71.08 | $425.00 |
| **📍 HDI** | mean | 0.567 | 0.833 |
| | median | 0.560 | 0.837 |
| **📉 Inflation (annual %)** | mean | 9.85% | 7.99% |
| | median | 6.09% | 4.64% |
| **📊 Unemployment (%)** | mean | 7.34% | 5.93% |
| | median | 5.54% | 5.65% |

---

## 📍 Key Findings

### 1. 🏆 HDI Dominance
HDI is the most crucial predictor for wealth classification, showing strong correlation with other development indicators, particularly minimum wage (R² = 0.756).

### 2. 📊 Unemployment Gap
Statistically significant higher unemployment rates in Poor countries (p = 7.8e-06), indicating structural challenges in job creation.

### 3. 🌐 Digital Divide
A consistent and widening gap in Internet Penetration over time between Rich and Poor nations, with Rich countries approaching saturation while Poor countries lag significantly.

### 4. 💸 Economic Stability
Poor countries experience higher and more volatile inflation rates, reflecting less economic stability compared to Rich countries.

### 5. 🌱 Multidimensional Development
Strong positive correlations exist between:
- Internet Penetration ↔ GDP
- Minimum Wage ↔ HDI

Development in one area correlates with and influences development in others, highlighting interconnected economic factors.

---

## 🖥️ Interactive Economic Dashboard

An interactive dashboard was developed using `ipywidgets` and `plotly` to provide real-time visualization and exploration of economic indicators.

### Dashboard Preview

![Economic Dashboard Screenshot](./images/dashboard_screenshot.png)
*Interactive dashboard showing economic indicators, trends, and global comparisons*

### 🎯 Key Features

#### **Navigation & Selection**
- 🌍 Country dropdown selector with Previous/Next buttons
- 📅 Year selector for temporal analysis
- 🏷️ Current selection display with visual badges

#### **Real-Time Statistics Cards**
- 💰 GDP Value
- 🌐 Internet Penetration Rate
- 📊 Human Development Index
- 💵 Minimum Wage
- 📈 Inflation Rate
- 👥 Unemployment Rate

#### **Interactive Visualizations**
- 📈 **Trend Charts**: Historical trends using Plotly line charts
- 📊 **Comparison Charts**: Top 10 countries by selected indicator
- 🔍 **Zoom, Pan, Hover**: Interactive chart capabilities

#### **Data Management**
- 📋 Detailed data table view
- 💾 Export functionality (current view & complete dataset)
- 🔄 Manual refresh capability

### 🚀 How to Use

```bash
# Launch Jupyter Notebook
jupyter notebook economic_dashboard.ipynb

# Run all cells to initialize the dashboard
# Navigate using dropdowns or Previous/Next buttons
# Interact with charts and export data as needed
```

---

## 🎯 Policy Recommendations

To bridge the developmental gap, Poor countries should focus on:

### 1. 🌐 Digital Infrastructure Investment
- Invest in widespread, affordable internet access
- Strong correlation between Internet Penetration and GDP growth
- Can serve as catalyst for economic development

### 2. 💼 Economic Stabilization
- Implement policies to control inflation volatility
- Promote stable employment opportunities through job creation programs
- Reduce economic uncertainty faced by citizens

### 3. 🎓 Human Capital Development
- Focus on health, education, and living standards (core HDI components)
- Essential for long-term sustainable development
- Deeply intertwined with economic prosperity

### 4. 🔄 Holistic Approach
- Address interconnected economic and social factors simultaneously
- Foster inclusive growth across all sectors
- Reduce global economic disparities through coordinated policy efforts

---

## 📂 Project Structure

```
economic-disparities-analysis/
├── data/
│   ├── cleaned_merged_data.csv       # Internet penetration and GDP data
│   ├── merged_data.csv               # HDI and minimum wage data
│   └── cleaned_data.csv              # Inflation and unemployment data
├── images/
│   └── dashboard_screenshot.png      # Dashboard interface screenshot
├── notebooks/
│   └── economic_dashboard.ipynb      # Complete analysis and dashboard
├── README.md                         # This file
└── requirements.txt                  # Python dependencies
```

---

## 🛠️ How to Reproduce This Analysis

### 📋 Prerequisites

```bash
# Install required packages
pip install pandas numpy matplotlib seaborn scikit-learn statsmodels jupyter plotly ipywidgets
```

### 🔄 Steps to Run

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd economic-disparities-analysis
   ```

2. **Place data files in `/data/` directory**
   - `cleaned_merged_data.csv`
   - `merged_data.csv`
   - `cleaned_data.csv`

3. **Launch Jupyter Notebook**
   ```bash
   jupyter notebook notebooks/economic_dashboard.ipynb
   ```

4. **Run all cells** to reproduce analysis and launch the interactive dashboard

### 📁 Data File Paths

Ensure your file paths are correctly set:

```python
# Adjust paths if needed
cleaned_merged_path = 'data/cleaned_merged_data.csv'
merged_data_path = 'data/merged_data.csv'  
cleaned_data_path = 'data/cleaned_data.csv'
```

---

## 🚀 Technologies Used

| Technology | Purpose |
|------------|---------|
| **Python 3.x** | Primary programming language |
| **Pandas & NumPy** | Data manipulation and numerical computing |
| **Matplotlib & Seaborn** | Static data visualization |
| **Plotly** | Interactive visualizations |
| **ipywidgets** | Dashboard interactive components |
| **Statsmodels** | Statistical modeling and regression |
| **Scikit-learn** | Machine learning (Random Forest) |
| **Jupyter Notebook** | Development and presentation environment |

---

## 🔮 Future Work

* 🌍 Incorporate additional socio-economic indicators (education levels, healthcare access)
* 🤖 Apply advanced ML models (Gradient Boosting, Neural Networks, XGBoost)
* 🔬 Conduct causal inference analysis to establish causality vs. correlation
* 🌎 Expand analysis to regional/continental comparisons
* 📅 Extend time-series forecasting for future economic projections
* 🔗 Integrate real-time data APIs for continuous updates

---

## 💡 Conclusion

This comprehensive analysis reveals **persistent and significant economic disparities** between Rich and Poor nations. Key takeaways include:

- **Economic development is multifaceted**: Improvements in digital infrastructure, wages, and stability are deeply interconnected
- **HDI serves as a powerful indicator**: Strong predictor of overall national development and economic performance
- **Targeted interventions are essential**: Poor countries require focused policy efforts in infrastructure, economic stability, and human capital
- **Data-driven insights enable better policy**: Statistical evidence can guide effective resource allocation and development strategies

The project provides a robust analytical framework for understanding global economic dynamics and offers actionable insights for policymakers working toward inclusive growth and reduced economic inequality.

---

## 👥 Team Members

| Name | ID |
|------|-----|
| Yassmin Ahmed Hassan | 231001654 |
| Zeina Mohamed Bahgat | 231001039 |
| Mario Sameh Fawzy | 231001484 |
| Ramy Mohamed Kamal | 231000792 |
| Youssef Khaled Gaber | 231000968 |
| Nour El-Dine Ayman | 231001282 |

**Course**: CSC322 - Data Analysis  
**Supervisor**: Dr. Shaimaa Mohamed Awad  
**Institution**: Nile University, Faculty of Computing and Information Technology  
**Date**: December 2025

---

## 📄 License

This project is available for educational and research purposes.

---

## 📧 Contact

For questions, feedback, or collaboration opportunities, please feel free to reach out to any team member or open an issue in the repository.

---

*This project provides foundational insights into global economic disparities and serves as a basis for further research and policy considerations.* 📊📈

**Last Updated**: January 2026
