# Prompt Log — Veri Bilimi Final Projesi
## Chronological record of AI prompts used during development

---

## PHASE 1: DATA LOADING & CLEANING

### Prompt #1 (Step: Project Setup & Data Loading)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"I have a credit risk dataset (credit_risk_dataset.csv) with 32,000+ records.
Help me set up a data science project structure with:
1. Import necessary libraries (numpy, pandas, matplotlib, seaborn)
2. Load the CSV file
3. Display basic info (shape, dtypes, head)"

**Output:** Import block + pd.read_csv() + df.info() + df.describe()
**Decision Made:** Used pandas for data manipulation, seaborn/matplotlib for visualization

---

### Prompt #2 (Step: Data Cleaning — Missing Values & Outliers)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Clean the credit risk dataset:
1. Handle missing values in person_emp_length (fill with 0)
2. Handle missing values in loan_int_rate (fill with median)
3. Remove outliers: person_age > 100, person_emp_length > 60
4. Show before/after counts for each cleaning step"

**Output:** fillna() operations + outlier filtering with boolean indexing
**Decision Made:** Used median for loan_int_rate to avoid skew from outliers,
filled emp_length with 0 assuming unemployed

---

### Prompt #3 (Step: Feature Engineering)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Create new engineered features for credit risk analysis:
1. loan_to_income_ratio = loan_amnt / person_income
2. risk column (High/Medium/Low) based on loan_to_income_ratio thresholds
3. emp_stability_ratio = person_emp_length / (person_age - 18)
4. loan_burden_index = loan_to_income_ratio × loan_int_rate
5. risk_adjusted_income (reduce by 30% if previous default on file)
6. customer_category (Young & High Potential, High Risk, Financial Giant, Standard)
7. credit_maturity_index = cb_person_cred_hist_length / person_age
8. red-flag binary column (previous default AND loan > $1000)"

**Output:** Multiple derived columns added to dataframe
**Decision Made:** These features capture financial stress and behavioral risk
beyond raw variables

---

## PHASE 2: EXPLORATORY DATA ANALYSIS (EDA)

### Prompt #4 (Step: EDA — Summary Statistics)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"For the credit risk dataset, generate summary statistics:
1. Total records and columns
2. Basic statistics (min, max, mean, std) for person_age,
   person_income, loan_amnt, loan_int_rate
3. Print results in a clear formatted output"

**Output:** df.describe() + formatted print statements
**Decision Made:** Focus on 4 key numerical variables for initial overview

---

### Prompt #5 (Step: EDA — Visualizations)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"For the credit risk dataset, create 5 visualizations:
1. Correlation matrix heatmap (seaborn) for all numerical variables
2. Bar chart showing risk level distribution (Low, Medium, High)
3. Scatter plot of Age vs Income with colors representing loan_status
4. Histogram of loan interest rate with mean and median lines
5. Distribution plot of loan to income ratio using KDE

For each visualization, also provide summary statistics
(mean, std, correlation, etc.)"

**Output:** 5 matplotlib/seaborn plots with accompanying statistics
**Key Finding:** loan_amnt & loan_int_rate correlation only 0.14 (weak!),
contrary to initial hypothesis. Risk distribution: Low=76.2%, High=22.6%,
Medium=4.1%

---

## PHASE 3: RESEARCH QUESTIONS

### Prompt #6 (Step: Research Question 1 — Credit History & Default)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Analyze credit history length vs default rate:
1. Group credit history into bins: 0-5, 5-10, 10-15, 15-20, 20+ years
2. Calculate default rate % for each group
3. Create bar chart with overall default rate reference line
4. Identify non-linear patterns"

**Output:** pd.cut() grouping + countplot + default rate statistics
**Key Finding:** NON-LINEAR relationship discovered! Default rate decreases
from 22.52% (0-5 years) to 20.78% (15-20 years) but SPIKES to 25.94%
at 20+ years. Hypothesis PARTIALLY REJECTED.
**Critical Thinking Applied:** Initially AI suggested hypothesis was confirmed,
but manual inspection of data revealed the spike at 20+ years — corrected
interpretation accordingly.

---

### Prompt #7 (Step: Research Question 2 — Loan Purpose & Default)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Analyze loan purpose vs default risk and interest rates:
1. Group by loan_intent
2. Calculate default rate % for each purpose
3. Calculate average interest rate for each purpose
4. Create side-by-side comparison charts
5. Identify which purposes are underpriced vs overpriced by bank"

**Output:** groupby aggregation + dual subplot comparison chart
**Key Finding:** DEBTCONSOLIDATION highest default (28.59%) but lowest
interest rate (10.98%) — bank is UNDERPRICING risky loans! VENTURE loans
safest (14.82%) and correctly priced low. Hypothesis REJECTED (expected
PERSONAL to be highest risk).

---

### Prompt #8 (Step: Research Question 3 — Feature Comparison)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Compare three engineered features as default predictors:
1. Calculate correlation of emp_stability_ratio with loan_status
2. Calculate correlation of loan_to_income_ratio with loan_status
3. Calculate correlation of loan_burden_index with loan_status
4. Create 3 scatter plots side by side (one per feature)
5. Group employment stability into quartiles and calculate default rate"

**Output:** Correlation table + 3-subplot scatter plot + quartile analysis
**Key Finding:** loan_burden_index (r=0.454) > loan_to_income_ratio (r=0.386)
>> emp_stability_ratio (r=-0.070). Hypothesis REJECTED — employment
stability is weakest predictor despite logical intuition.
**Bug Fixed:** Originally plotted only 2 features, missing loan_burden_index.
Corrected to 3 subplots to match research question scope.

---

## PHASE 4: CLASSIFICATION MODEL

### Prompt #9 (Step: Model Building — Logistic Regression)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Build a Logistic Regression model to predict loan_status:
1. Encode loan_intent using pd.get_dummies (drop_first=True)
2. Select 11 features based on RQ findings:
   loan_burden_index, loan_to_income_ratio, loan_int_rate,
   cb_person_cred_hist_length, person_age, emp_stability_ratio,
   and all loan_intent encoded columns
3. Split data 80/20 train/test with stratify=y
4. Scale features using StandardScaler
5. Train LogisticRegression(random_state=42, max_iter=1000)
6. Generate predictions and probability scores"

**Output:** Trained model + predictions stored in y_pred, y_pred_proba
**Decision Made:** Used stratify=y to maintain class balance in split.
Used max_iter=1000 to ensure convergence.

---

### Prompt #10 (Step: Model Evaluation)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Evaluate the logistic regression model with:
1. Accuracy score and ROC-AUC score
2. Full classification report (precision, recall, f1-score)
3. Confusion matrix heatmap (seaborn)
4. ROC curve plot with AUC score
5. Feature importance bar chart using model coefficients"

**Output:** 83.61% accuracy, ROC-AUC=0.8323, confusion matrix,
ROC curve, feature importance chart
**Key Finding:** Default recall only 41% — model misses 59% of actual
defaults due to class imbalance (78% good loans vs 22% defaults)

---

### Prompt #11 (Step: Model Interpretation & Limitations)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Interpret the model results:
1. Why is default recall only 41% despite 83% accuracy?
2. Why does loan_burden_index have a NEGATIVE coefficient (-1.20)
   despite being positively correlated with default?
3. What does the confusion matrix mean in real banking context?
4. How do feature coefficients confirm or contradict our RQ findings?
5. What are the model limitations and recommendations?"

**Output:** Detailed interpretation of class imbalance, multicollinearity
explanation, business impact analysis
**Key Finding:** loan_burden_index negative coefficient explained by
multicollinearity with loan_to_income_ratio and loan_int_rate.
loan_to_income_ratio confirmed as TRUE strongest predictor (coef=+2.05)

---

## PHASE 5: DEBUGGING & CORRECTIONS

### Prompt #12 (Step: Bug Fixes & Corrections)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Fix the following issues found during development:
1. import matplotlib as plt → should be import matplotlib.pyplot as plt
2. categorize_customers function using np.median(row['person_income'])
   on a scalar value → should be np.median(df['person_income'])
3. RQ1 finding stated hypothesis confirmed but data showed spike
   at 20+ years — correct the interpretation
4. RQ3 title said comparing 2 things but compared 3 — fix visualization"

**Output:** Corrected imports, fixed function logic, updated interpretations
**Learning:** Always verify AI-generated interpretations against actual data.
Critical thinking is essential — AI can make logical errors in analysis.

---

### Prompt #13 (Step: Visualization Improvements)
**Tool Used:** Claude (Anthropic)
**Prompt:**
"Improve visualizations:
1. Add plt.xticks(rotation=45) for long x-axis labels
2. For subplot axes use axes[0].tick_params(axis='x', rotation=45)
3. Add reference lines (axhline) to bar charts
4. Ensure plt.tight_layout() on all plots to prevent label cutoff"

**Output:** Improved readability across all visualizations
**Decision Made:** Used axes[i].tick_params() for subplots,
plt.xticks() for single plots

---

## SUMMARY

| Phase | Prompts | Key Outputs |
|-------|---------|-------------|
| Data Loading & Cleaning | #1, #2 | Clean dataset, outliers removed |
| Feature Engineering | #3 | 8 new features created |
| EDA | #4, #5 | 5 visualizations, key correlations |
| Research Questions | #6, #7, #8 | 3 RQs answered, 3 hypotheses tested |
| Modelling | #9, #10, #11 | 83.61% accuracy, ROC-AUC=0.8323 |
| Debugging | #12, #13 | Bugs fixed, interpretations corrected |

**Total Prompts: 13**
**Tool Used Throughout: Claude (Anthropic) — claude.ai**