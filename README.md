# Cars Price Regression Analysis

## 1. Project Goal and Problem Definition

### 1.1 Dataset Selection
**Dataset**: USA Cars Dataset  
**Source**: Used car auction data from United States  
**Original size**: 2499 observations, 12 variables  
**Size after cleaning**: 2068 observations, 8 variables  

### 1.2 Dataset Characteristics
**Variables in dataset**:
- **Price** - Vehicle sale price in USD
- **Year** - Vehicle model year  
- **Brand** - Car manufacturer
- **Model** - Vehicle model
- **Color** - Vehicle color
- **State/Country** - Location where vehicle is available
- **Mileage** - Vehicle mileage (miles driven)
- **Vin** - Vehicle identification number
- **Title_status** - Legal status of vehicle
- **Lot** - Auction lot number
- **Condition** - Vehicle condition description

### 1.3 Analysis Topic and Goal
**Topic**: Analysis of factors affecting used car prices in USA

**Analysis objectives**:
- Identify key factors determining used car prices
- Build predictive model for price prediction based on vehicle characteristics  
- Compare effectiveness of different regression algorithms for car price prediction

### 1.4 Dependent Variable
**Dependent variable**: Price - vehicle sale price in USD

**Independent variables**:
- Year - vehicle model year (transformed to years from oldest model year)
- Brand - car manufacturer
- Model - vehicle model
- Color_group - vehicle color group
- State - vehicle location state
- Mileage - vehicle mileage
- Title_status - vehicle legal status

### 1.5 Data Preparation
**Transformations performed**:
- Removed unnecessary columns: Unnamed: 0, vin, condition, lot, country
- Brand filtering: Removed brands with <100 cars
- Year filtering: Limited to vehicles >2000
- Location filtering: Kept only USA vehicles (removed 7 from Canada)
- Removed suspiciously low-priced vehicles: Kept vehicles above $1000
- Color grouping: Created 6 color groups from 20+ original colors
- Year transformation: Converted year to vehicle age on market
- Standardization and encoding: StandardScaler for numerical variables, OneHotEncoder for categorical

## 2. Statistical Description of Analyzed Features

### 2.1 Descriptive Statistics for Dependent Variable
**Price - basic statistics**:
- Mean: ~$19,300
- Median: $17,900
- Standard deviation: ~$11,450
- Minimum: $1,150
- Maximum: $67,000
- Distribution: Right-skewed with long tail

### 2.2 Numerical Variables Characteristics
**Mileage**:
- Mean: ~49,430 miles
- Median: 35,233 miles
- Range: 0 - 999,999 miles
- Observation: Strong negative correlation with price (-0.42) - lower mileage means more expensive cars

**Year (after transformation)**:
- Range: 0-16 years (2001-2017)
- Observation: Positive correlation with price (0.42) - newer cars more expensive

### 2.3 Categorical Variables Characteristics
**Brand**:
- Ford: ~54% of dataset, highest median price (~$22,000)
- Dodge: ~18% of dataset
- Nissan: ~14% of dataset, lowest median price (~$11,000)
- Chevrolet: ~12% of dataset

**Title_status**:
- Clean: ~85% - vehicles without damage
- Salvage insurance: ~15% - damaged vehicles
- Observation: "Clean" vehicles are 3-5x more expensive than damaged ones

## 3. Statistical Inference and Regression Model

### 3.1 Hypothesis Verification and Distribution Analysis
**Normality test for dependent variable**:
- Price distribution is right-skewed
- Presence of outliers in upper price ranges
- Conclusion: Data doesn't have normal distribution, but regression models are robust to this assumption with large samples

### 3.2 Correlation Analysis
**Correlations with price**:
- Model: 0.75
- Year: 0.43  
- Mileage: -0.42
- State: 0.39
- Title_status: 0.32
- Brand: 0.29
- Color_group: 0.09
- Country: 0.0

**Key observations**:
- Specific car models have biggest impact on price
- Mileage has strong negative impact on price
- Brand has smaller impact than specific model

### 3.3 Dataset Split
Data was split into training (80%) and test (20%) sets using train_test_split. KFold method with random shuffle was used for model validation.

### 3.4 Building and Comparing Regression Models
**Model performance on test data (R² Score)**:
- Linear Regression: 0.64
- Lasso: 0.65
- Ridge: 0.65
- Support Vector Machine: 0.07
- Random Forest Regression: 0.50
- XGBoost: 0.72

### 3.5 Best Model Interpretation (XGBoost)
**Best XGBoost parameters**:
- learning_rate: 0.1
- max_depth: 10
- n_estimators: 700
- random_state: 42

**Key findings**:
- 19/20 most important features are categorical variables
- Specific models dominate over technical parameters
- Brand/model prestige outweighs technical specifications
- Model uses 150+ features after OneHot encoding

### 3.6 Prediction and Model Quality Assessment
**Test set results**:
- R² Score: 0.72 (72% of price variance explained by model)
- Cross-validation score: 0.69 ± 0.03
- Interpretation: Model has good predictive ability and generalizes well to new data

**Training set results**:
- R² Score: 0.85 (slight overfitting)
- Difference: 0.13 (acceptable for tree-based models)

## 4. Results Summary and Conclusions

Brand and model are main price determinants, mileage is important but has less impact than brand prestige, damaged vehicles are significantly cheaper.

The project confirmed the hypothesis that in the used car market, factors related to brand and model prestige have greater impact on price than purely technical vehicle parameters. XGBoost model achieved satisfactory prediction accuracy (R²=0.72), demonstrating practical value of applied data analysis methods in vehicle valuation context.
