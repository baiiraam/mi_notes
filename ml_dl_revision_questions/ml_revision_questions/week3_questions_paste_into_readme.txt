# 📚 WEEK 3 — COMPLETE STUDY GUIDE
## All Exercises with Answers in Spoiler Format

---

# SECTION 1: DATA PREPARATION (Practical Issues in Data Preparation)

---

## Exercise DP-1: Why Data Preparation Matters

| Question | Your Answer |
|----------|-------------|
| 1. What percentage of a data scientist's time is spent on data preparation? | |
| 2. What is the estimated annual cost of bad data quality in the US? | |
| 3. What is the #1 factor in failed ML projects? | |
| 4. What is the "Garbage in, garbage out" principle? | |
| 5. What goes wrong without proper data preparation? (3 things) | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Time spent on data prep | **60–80%** of a data scientist's time |
| 2. Annual cost of bad data | **~$3 trillion** in the US |
| 3. #1 factor in failed ML projects | **Bad data quality** |
| 4. "Garbage in, garbage out" | The quality of your output is strictly limited by the quality of your input. |
| 5. What goes wrong without data prep | **Models learn from noise** instead of signal → poor generalization; **Missing values** cause crashes or silent bias; **Unencoded categories** are ignored or misinterpreted by algorithms; **Misleading visualizations** lead to wrong business decisions. |

</details>

---

## Exercise DP-2: The Data Preparation Pipeline

| Question | Your Answer |
|----------|-------------|
| 1. List the 6 steps of the data preparation pipeline in order. | |
| 2. Why is the pipeline iterative? | |
| 3. What is the key principle of the pipeline? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Six steps | **Step 1**: Raw Data (collected, unfiltered source data). **Step 2**: Inspect (profile and understand shape and quality). **Step 3**: Clean (remove errors, duplicates, outliers). **Step 4**: Impute (handle missing values). **Step 5**: Encode (convert categories to numbers). **Step 6**: Visualize (explore patterns before modeling). |
| 2. Why iterative | You will often **loop back** after discovering new issues. |
| 3. Key principle | This pipeline is iterative — you will often loop back after discovering new issues. |

</details>

---

## Exercise DP-3: Common Data Quality Issues

| Question | Your Answer |
|----------|-------------|
| 1. What are the 5 common data quality issues? | |
| 2. Give an example of inconsistent formatting. | |
| 3. Give an example of a wrong dtype issue. | |
| 4. What is a sentinel value? Give examples. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Five common issues | **Missing Values** (NaN, NULL, empty fields, sentinel values like -999). **Duplicates** (exact or near-duplicate rows from merges or re-imports). **Outliers** (extreme values from measurement error or rare events). **Inconsistent Format** ('USA', 'U.S.A', 'us' — same value, different representations). **Wrong Dtype** (zip codes stored as floats, dates as strings). **Categorical Encoding** (text labels algorithms cannot directly process). |
| 2. Inconsistent formatting example | 'USA', 'U.S.A', 'us', 'United States' — same value, different representations. |
| 3. Wrong dtype example | Zip codes stored as floats (10001.0 instead of '10001'), dates stored as strings. |
| 4. Sentinel value | A value that looks valid but means "no data" (e.g., -999, -1, 0, 9999, 'N/A', 'unknown'). |

</details>

---

## Exercise DP-4: Data Cleaning — Duplicates

| Question | Your Answer |
|----------|-------------|
| 1. What are the three types of duplicates? | |
| 2. How do you handle exact duplicates in pandas? | |
| 3. How do you handle key-field duplicates? | |
| 4. What is the decision point before deleting duplicates? | |
| 5. Why shouldn't you blindly delete duplicates? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Three types of duplicates | **Exact duplicates**: identical rows on all columns. **Key-field duplicates**: same ID but slightly different attributes (typos, case differences). **Near-duplicates**: fuzzy matches (e.g., 'Jon Smith' vs 'John Smith'). |
| 2. Handling exact duplicates | `df = df.drop_duplicates()` — remove all exact duplicate rows. |
| 3. Handling key-field duplicates | `df = df.drop_duplicates(subset=["customer_id"], keep="last")` — keep last record per customer ID. |
| 4. Decision point before deleting | **Do not blindly delete** — understand WHY duplicates exist. |
| 5. Why not blindly delete | **Legitimate**: same customer, two different orders. **Accidental**: merge errors, system re-imports. Document every deletion with a reason. |

</details>

---

## Exercise DP-5: Outlier Detection Methods

| Question | Your Answer |
|----------|-------------|
| 1. What is an outlier? | |
| 2. How does the Z-score method work? What is it best for? | |
| 3. How does the IQR (box plot) method work? What is it best for? | |
| 4. How does Isolation Forest work for outlier detection? | |
| 5. What are the 5 outlier handling strategies? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Outlier definition | A data point that differs significantly from other observations. They may represent errors or genuinely rare events. |
| 2. Z-score method | Flag points more than **2–3 standard deviations** from the mean: `z = (x − μ) / σ`, flag if `\|z\| > 3`. **Best for**: normally distributed data. |
| 3. IQR method | **Q1** = 25th percentile, **Q3** = 75th percentile, **IQR** = Q3 − Q1. Lower = Q1 − 1.5×IQR, Upper = Q3 + 1.5×IQR. **Best for**: skewed data. |
| 4. Isolation Forest | Randomly selects a feature and threshold to isolate points. Points with **shorter path lengths** to isolate are outliers. Collection of trees (e.g., 100) computes average path length. |
| 5. Five handling strategies | **Remove**: drop the row (if error confirmed, dataset large). **Impute**: replace with median/mean. **Winsorize**: cap values at threshold (e.g., 5th–95th percentile). **Separate**: build model with and without outliers; compare. **Transform**: apply log, sqrt, or Box-Cox to reduce influence. **Keep**: some domains (fraud, rare disease) need outliers. |

</details>

---

## Exercise DP-6: Inconsistent Formatting & Data Types

| Question | Your Answer |
|----------|-------------|
| 1. Why is inconsistent formatting a problem? | |
| 2. How would you standardize country names? | |
| 3. How would you parse messy dates? | |
| 4. How would you clean a salary column with '$' and 'K'? | |
| 5. What are the key string cleaning techniques? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why inconsistent formatting is a problem | Inconsistency **silently breaks groupBy, joins, and model features**. The same value appears in dozens of forms. |
| 2. Standardize country names | `country_map = {"usa":"USA", "u.s.a.":"USA", "us":"USA"}` then `df["country"] = df["country"].str.lower().map(country_map)` |
| 3. Parse messy dates | `df["date"] = pd.to_datetime(df["date"], infer_datetime_format=True)` |
| 4. Clean salary column | `df["salary"].astype(str).str.replace(r'[$,K]', '', regex=True).str.strip().astype(float)` |
| 5. String cleaning techniques | `.str.strip()` (remove whitespace), `.str.lower()/.title()` (normalize case), `.str.extract(regex)` (pull structured data), `.str.replace(regex)` (remove unwanted characters), `.str.contains()` (flag rows for review). |

</details>

---

## Exercise DP-7: Missing Values — Types & Detection

| Question | Your Answer |
|----------|-------------|
| 1. What are the three types of missing values? | |
| 2. What is MCAR? Give an example. | |
| 3. What is MAR? Give an example. | |
| 4. What is MNAR? Give an example. | |
| 5. Why does the type of missingness matter? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Three types of missingness | **MCAR** (Missing Completely at Random), **MAR** (Missing at Random), **MNAR** (Missing Not at Random). |
| 2. MCAR with example | Missingness is **unrelated to any variable**. Example: sensor randomly drops 5% of readings. **Low bias, safe to delete rows**. Test: Little's MCAR test (p > 0.05 means MCAR). |
| 3. MAR with example | Missingness depends on **other observed variables**. Example: men less likely to report weight; depends on 'gender' column. **Imputation valid if you include predictors**. Most common in practice. |
| 4. MNAR with example | Missingness depends on the **missing value itself**. Example: high earners skip the salary field. **Highest bias risk, imputation unreliable**. Requires domain knowledge or model-based approach. |
| 5. Why it matters | Using the **wrong strategy introduces bias**. Deleting rows is only safe under MCAR. Under MAR/MNAR, deletion biases your model. When in doubt, impute. |

</details>

---

## Exercise DP-8: Missing Value Imputation Strategies

| Question | Your Answer |
|----------|-------------|
| 1. What are the simple imputation methods? | |
| 2. What are the advanced imputation methods? | |
| 3. What is the missingness indicator technique? | |
| 4. When would you add a missingness indicator? | |
| 5. What are the deletion strategies? When are they appropriate? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Simple imputation | **Mean** (symmetric numerical data) — distorts distribution, reduces variance. **Median** (skewed numerical data) — still collapses all missing to one value. **Mode** (categorical data) — may over-represent dominant class. **Constant** (category 'Unknown' or 0 for counts) — creates artificial category or spike at 0. |
| 2. Advanced imputation | **KNN Imputation**: find K nearest neighbors (rows most similar on non-missing features) and use their average/mode. **Iterative Imputation (MICE)**: models each feature with missing values as a function of others; iterates until convergence. **Forward/Backward Fill**: for time series data only. |
| 3. Missingness indicator | Add a binary column recording whether the value was missing: `df["income_was_missing"] = df["income"].isnull().astype(int)`. |
| 4. When to add | When the **FACT of being missing predicts your target** (MNAR). Example: applicants who don't disclose income are higher risk. |
| 5. Deletion strategies | **Listwise Deletion**: drop all rows with any missing (complete-case analysis). **Unbiased if MCAR**. **Column Deletion**: drop column if missing > threshold (e.g., >40%). **When NOT to delete**: dataset is small (N < 1,000), missing rate > 5% (risk of bias), MNAR suspected, feature is highly predictive. |

</details>

---

## Exercise DP-9: Missing Value Decision Thresholds

| Question | Your Answer |
|----------|-------------|
| 1. < 5% missing → recommended strategy | |
| 2. 5–20% missing → recommended strategy | |
| 3. 20–40% missing → recommended strategy | |
| 4. > 40% missing → recommended strategy | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. < 5% missing | **Almost any strategy works**; simple imputation is fine. |
| 2. 5–20% missing | **Impute carefully**; consider multiple imputation if MNAR is suspected. |
| 3. 20–40% missing | **Imputation risky**; consider adding a missingness indicator column. |
| 4. > 40% missing | **Consider dropping the column**; investigate why so much is missing. |

</details>

---

## Exercise DP-10: Encoding Categorical Variables

| Question | Your Answer |
|----------|-------------|
| 1. Why must we encode categorical variables? | |
| 2. What are the four types of categorical variables? | |
| 3. What is Label Encoding? When is it appropriate? | |
| 4. What is Ordinal Encoding? When is it appropriate? | |
| 5. What is One-Hot Encoding? When is it appropriate? | |
| 6. What is the "dummy variable trap"? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why encode | Machine learning algorithms operate on numbers. Categorical text values must be converted before training. Most sklearn models throw TypeError on strings. Distance metrics (KNN, SVM) require numbers. |
| 2. Four types | **Nominal**: no inherent order (Color: Red, Blue, Green) → One-Hot Encoding. **Ordinal**: meaningful order, uneven gaps (Size: S < M < L < XL) → Ordinal/Label Encoding. **Binary**: only 2 values (Churned: Yes/No) → Binary (0/1). **High-Cardinality**: many unique values (City: 1000+ cities) → Target/Freq Encoding. |
| 3. Label Encoding | Assigns an integer to each unique category (e.g., 'USA'→0, 'Canada'→1, 'UK'→2). **Implies ordering** — use only for tree-based models or truly ordinal data. |
| 4. Ordinal Encoding | Maps categories to integers in a user-defined order. **Correct when a real order exists**: `df['size'] = df['size'].map({'S':0, 'M':1, 'L':2, 'XL':3})`. |
| 5. One-Hot Encoding | Creates a binary column for each unique category. The model sees independent features with no implied ordering — standard for nominal variables. Use `drop_first=True` to avoid multicollinearity. |
| 6. Dummy variable trap | When you have K categories and create K dummy columns, they are perfectly collinear (sum to 1). **Fix**: drop one column (`drop_first=True`). |

</details>

---

## Exercise DP-11: Advanced Encoding Methods

| Question | Your Answer |
|----------|-------------|
| 1. What is Target Encoding? | |
| 2. What is the risk of Target Encoding? | |
| 3. How do you prevent leakage in Target Encoding? | |
| 4. What is Frequency Encoding? | |
| 5. What are the pros and cons of Frequency Encoding? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Target Encoding | Replace each category with the **mean of the target variable** for that category. Example: City → avg churn rate for that city (New York → 0.42). |
| 2. Risk of Target Encoding | **Leaks target information!** The mean target per category may include data from validation/test if not done properly. |
| 3. Prevent leakage | Use **K-Fold cross-fitting**: compute target means on training folds only, apply to validation fold. Never compute target means on full training set and then use for validation. |
| 4. Frequency Encoding | Replace each category with its **frequency** (count or proportion) in the training set. Example: City → (count in dataset) or (count / total rows). |
| 5. Pros and cons of Frequency Encoding | **Pros**: No target leakage. **Cons**: Different cities with the same frequency get the same encoding (loses distinction). |

</details>

---

## Exercise DP-12: Choosing an Encoding Strategy

| Question | Your Answer |
|----------|-------------|
| 1. Binary feature (yes/no) → encoding | |
| 2. Nominal, few categories (< 15) → encoding | |
| 3. Ordinal with known order → encoding | |
| 4. High-cardinality nominal → encoding | |
| 5. Tree-based model → encoding | |
| 6. Linear model / SVM / Neural Net → encoding | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Binary feature | **Binary (0/1)** — simplest; no extra columns. |
| 2. Nominal, few categories | **One-Hot Encoding** — no false ordering implied. |
| 3. Ordinal with known order | **Ordinal Encoding** — preserves meaningful ranking. |
| 4. High-cardinality nominal | **Target or Frequency Encoding** — avoids column explosion. |
| 5. Tree-based model | **Label / Ordinal Encoding** — trees split on values; OHE wastes depth. |
| 6. Linear model / SVM / Neural Net | **One-Hot Encoding** — linear combination needs dummy variables. |

</details>

---

## Exercise DP-13: Discussion Questions — Data Preparation

### Discussion Question 1

| Question | Your Answer |
|----------|-------------|
| You receive a dataset where 35% of the 'income' column is missing. The missing values come almost entirely from self-employed respondents. Which missingness mechanism is this? How would you handle it? | |

<details>
<summary>📖 Click for Answers</summary>

**Answer:** This is **MAR (Missing at Random)** — missingness depends on 'employment_status' (observed variable).

**Handling strategy:**
- **Do NOT delete** — 35% is too high; deletion would bias the model
- **Impute with median income by employment status** — self-employed get median of self-employed, employed get median of employed
- **Add a missingness indicator** — `income_was_missing` column to capture the pattern that self-employed respondents didn't disclose income (this may be predictive!)
- **Consider Multiple Imputation (MICE)** — use other variables (age, education, location) to predict income
- **Downstream model matters**: tree models handle missingness better; linear models need careful imputation

</details>

---

### Discussion Question 2

| Question | Your Answer |
|----------|-------------|
| A colleague one-hot encodes the 'city' column, which has 800 unique values. The training set now has 812 columns. What problems does this cause, and what would you recommend instead? | |

<details>
<summary>📖 Click for Answers</summary>

**Problems caused:**
- **Curse of dimensionality** — distance metrics become meaningless; models need exponentially more data
- **Sparsity** — most rows have 0 in 799 of 800 columns; waste of memory and compute
- **Overfitting** — rare cities get their own feature with few examples
- **Slow training** — 800 extra features = much slower model

**Recommendations:**
- **Frequency Encoding** — replace city with count or proportion
- **Target Encoding** — replace with target mean per city (use K-fold to prevent leakage)
- **Group rare cities** — keep top 20–50 cities, collapse rest into "Other"
- **For tree models**: use Label Encoding — trees can handle high-cardinality without OHE explosion

</details>

---

### Discussion Question 3

| Question | Your Answer |
|----------|-------------|
| A model trained on cleaned data achieves AUC = 0.92 in validation but only 0.67 in production. Data prep is suspected. What are three possible causes and how would you investigate? | |

<details>
<summary>📖 Click for Answers</summary>

**Three possible causes:**
1. **Training-serving skew** — transformations applied differently between train and inference
2. **Target encoding leakage** — target means computed on full training set (including validation data)
3. **Imputation strategy mismatch** — different imputation between train and inference

**How to investigate:**
- Check: were all transformations wrapped in a **Pipeline**? If not, manual steps likely differ
- Check: was target encoding done **inside cross-validation**? If computed on full dataset, it's leakage
- Check: are imputation values (mean/median) from **training set only**? Inference should use training-derived values
- Check: are outlier capping thresholds **hard-coded** vs. data-driven (from training)?

</details>

---

### Discussion Question 4

| Question | Your Answer |
|----------|-------------|
| You are preparing a dataset for a fraud detection model. 99% of transactions are legitimate; 1% are fraud. How does this affect your data cleaning and missing value decisions? | |

<details>
<summary>📖 Click for Answers</summary>

**Key considerations:**
- **Outliers are signal, not noise!** Fraud transactions ARE outliers. Do NOT remove them as outliers — that would remove all fraud cases!
- **Missingness may differ by class** — fraudsters may leave fields blank intentionally. Check: does missingness correlate with fraud? If yes, add a missingness indicator.
- **Minority class visualization** — use separate histograms/boxplots for fraud vs. legitimate to see patterns; don't let majority class drown out the minority.
- **Evaluation metrics** — accuracy is useless (99% dummy classifier). Use **precision, recall, F1, AUC-ROC, and PR-AUC**.
- **Class imbalance** — consider resampling (SMOTE), class weights, or specialized metrics.

</details>

---

### Discussion Question 5

| Question | Your Answer |
|----------|-------------|
| In what order should you perform the steps in the data preparation pipeline? Does the order matter? Give examples where the order changes the result. | |

<details>
<summary>📖 Click for Answers</summary>

**Recommended order:**
1. **Inspect** first — understand the data before changing anything
2. **Clean** duplicates and inconsistent formatting BEFORE imputation
3. **Handle outliers** BEFORE or DURING imputation (outliers affect mean)
4. **Impute** missing values
5. **Encode** categories
6. **Visualize** after transformations to verify

**Where order matters:**
- **Outlier removal before mean imputation** — if you remove outliers first, the mean changes; imputation after removal gives different values
- **Duplicate detection before string normalization** — 'USA' and 'us' are duplicates but won't be detected if normalized first (though normalization is usually better to do first)
- **Encoding before imputation** — with sklearn pipelines, impute then encode; but for target encoding, you must ensure no leakage

**Is there always a "correct" order?** No — it's context-dependent. But some principles: clean before impute, impute before encode, and **always fit on training data only**.

</details>

---

# SECTION 2: FEATURE ENGINEERING (3.2 Feature Engineering)

---

## Exercise FE-1: What is Feature Engineering?

| Question | Your Answer |
|----------|-------------|
| 1. Define feature engineering. | |
| 2. Who said "Applied ML is basically feature engineering"? | |
| 3. Raw feature: signup_date → engineered features? | |
| 4. Why does feature engineering matter more than algorithm choice? | |
| 5. List the 6 core categories of feature engineering. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Feature engineering definition | The process of using **domain knowledge** to create, transform, or select input variables that make machine learning algorithms work better. |
| 2. Quote attribution | **Andrew Ng** — "Coming up with features is difficult, time-consuming, and requires expert knowledge. Applied ML is basically feature engineering." |
| 3. Raw → engineered | signup_date: '2022-03-15' → **account_age_days**: 655, **days_since_login**: 9, **is_pro_plan**: 1, **avg_order_value**: 60.04, **orders_per_month**: 2.1 |
| 4. Why features matter more than algorithm | A well-engineered feature can matter more than the choice of algorithm. |
| 5. Six core categories | **1. Transformations**: scale, log, sqrt, polynomial. **2. Interactions**: multiply, ratio, diff. **3. Temporal**: time parts, lags, rolling windows. **4. Text/NLP**: TF-IDF, embeddings, sentiment. **5. Aggregations**: group-level stats. **6. Domain-Specific**: expert knowledge encoded as features. |

</details>

---

## Exercise FE-2: The Feature Engineering Mental Model

| Question | Your Answer |
|----------|-------------|
| 1. What is the model-centric (naive) approach to a timestamp? | |
| 2. What is the feature-centric (expert) approach to a timestamp? | |
| 3. What are the 4 questions to ask when engineering features? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Model-centric approach | Give raw timestamp (e.g., 1704153600). **Model must discover** months, weekdays, hours from raw integers alone. Requires enormous data to learn implicitly. |
| 2. Feature-centric approach | Engineer: **hour_of_day, day_of_week, is_weekend, is_holiday, days_since_last_purchase**. Model immediately has actionable signals. |
| 3. Four questions | **#1**: What does a human expert look at in this column that a model can't see directly? **#2**: Is there a ratio, difference, or combination with another column that encodes a business rule? **#3**: Does the column's meaning change depending on context (time, group, or category)? **#4**: Are there hidden non-linearities? (e.g., salary effect on spending isn't linear) |

</details>

---

## Exercise FE-3: Feature Scaling Methods

| Question | Your Answer |
|----------|-------------|
| 1. What is Min-Max Normalization? Formula? Best for? | |
| 2. What is Standardization (Z-score)? Formula? Best for? | |
| 3. What is Robust Scaling? Formula? Best for? | |
| 4. Which scaling method is most commonly used? | |
| 5. Which scaling method is sensitive to outliers? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Min-Max Normalization | **Formula**: `x' = (x − min) / (max − min)` — scales to [0, 1] range. **Best for**: neural networks, KNN, SVM, image data. **Sensitive to outliers** — one extreme value compresses all others. |
| 2. Standardization (Z-score) | **Formula**: `x' = (x − μ) / σ` — mean = 0, std = 1. **Best for**: linear/logistic regression, PCA, SVM. **Robust to outliers**. **Most commonly used method**. |
| 3. Robust Scaling | **Formula**: `x' = (x − median) / IQR` — uses median & IQR, resistant to outliers. **Best for**: data with outliers you cannot remove. Doesn't bound values to a fixed range. |
| 4. Most commonly used | **Standardization (Z-score)** |
| 5. Sensitive to outliers | **Min-Max Normalization** — one extreme value compresses all others. |

</details>

---

## Exercise FE-4: Log & Power Transforms

| Question | Your Answer |
|----------|-------------|
| 1. What types of data benefit from log transforms? | |
| 2. What is Log1p and when would you use it? | |
| 3. What is Box-Cox transform? | |
| 4. What is Yeo-Johnson transform? | |
| 5. When would you use reciprocal transform? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Data benefiting from log transforms | **Right-skewed** features (income, prices, counts). Reduces skew, stabilizes variance, improves linear model fit. |
| 2. Log1p | `log(x + 1)` — **use when data includes zero values** (counts, frequencies). Handles log(0) which is undefined. |
| 3. Box-Cox | `((x^λ − 1)/λ)` — finds **optimal λ automatically**. Data must be positive. Use `PowerTransformer(method='box-cox')`. |
| 4. Yeo-Johnson | Modified Box-Cox — **handles zero and negative values** too. Use `PowerTransformer(method='yeo-johnson')`. |
| 5. Reciprocal transform | `1/x` — **when small values need to have large impact**. |

</details>

---

## Exercise FE-5: Binning & Discretization

| Question | Your Answer |
|----------|-------------|
| 1. What is Equal-Width Binning? Risk? | |
| 2. What is Equal-Frequency (Quantile) Binning? | |
| 3. What is Domain-Knowledge Binning? | |
| 4. Give a code example for FICO score bins. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Equal-Width Binning | Divide range into N equal-width intervals. Age → [0-20), [20-40), [40-60), [60+). **Risk**: sparse bins if data is skewed. |
| 2. Equal-Frequency Binning | Each bin holds the **same number of observations** (quartile bins: Q1, Q2, Q3, Q4). **Better for skewed distributions**. |
| 3. Domain-Knowledge Binning | Bin boundaries defined by **business rules**. Most interpretable. Example: child(<13), teen(13-17), adult(18-64), senior(65+). |
| 4. FICO score bins example | `fico_bins = [300, 580, 670, 740, 800, 850]`. `df["credit_tier"] = pd.cut(df["fico_score"], bins=fico_bins, labels=["Poor","Fair","Good","VeryGood","Exceptional"])` |

</details>

---

## Exercise FE-6: Polynomial & Ratio Features

| Question | Your Answer |
|----------|-------------|
| 1. What do polynomial features capture? | |
| 2. Give examples of ratio features in finance. | |
| 3. Give examples of ratio features in retail. | |
| 4. Why do ratios often outperform raw values? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Polynomial features capture | **Non-linear relationships** by adding powers and cross-products. `x²` captures U-shaped effects (age vs. income). `x₁ × x₂` creates interaction terms. |
| 2. Finance ratio examples | **Debt-to-Income** = total_debt / annual_income. **Credit Utilization** = balance / credit_limit. **YOY Growth** = (rev_2024 − rev_2023) / rev_2023. |
| 3. Retail ratio examples | **Effective price** = price × (1 − discount). **Conversion rate** = conversions / impressions. |
| 4. Why ratios outperform raw values | Domain knowledge encoded as arithmetic. They capture **relative relationships** that raw values alone don't reveal. Often ratios are more predictive than the raw absolute values. |

</details>

---

## Exercise FE-7: Temporal Feature Engineering

| Question | Your Answer |
|----------|-------------|
| 1. What temporal features can you extract from a timestamp? | |
| 2. Why is cyclical encoding needed for time features? | |
| 3. How do you cyclically encode hours? | |
| 4. How do you cyclically encode months? | |
| 5. What are lag features? | |
| 6. What are rolling window statistics? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Temporal features from timestamp | **year, month, day_of_week, is_weekend, hour_of_day, quarter, is_month_start, is_holiday**. Each captures different seasonal/cyclic patterns. |
| 2. Why cyclical encoding? | Hours, days, months are **cyclic** — hour 23 is close to hour 0, but numerically they're far apart. Sin/cos encoding preserves circular structure. |
| 3. Cyclical encoding for hours | `sin_hour = sin(2π × hour / 24)`, `cos_hour = cos(2π × hour / 24)`. Hour 0 and hour 24 now map to the same point. |
| 4. Cyclical encoding for months | `sin_month = sin(2π × month / 12)`, `cos_month = cos(2π × month / 12)`. Dec (12) and Jan (1) become adjacent. |
| 5. Lag features | Look backward in time: **sales_lag1** = yesterday's sales, **sales_lag7** = same day last week, **sales_lag30** = same day last month. Captures autocorrelation and seasonality. |
| 6. Rolling window statistics | Rolling aggregations over a window: **rolling_mean_7d** = 7-day average, **rolling_std_7d** = 7-day volatility, **rolling_max_30d** = 30-day peak. Captures trends, volatility, momentum. |

</details>

---

## Exercise FE-8: Interaction Features

| Question | Your Answer |
|----------|-------------|
| 1. What is an interaction feature? | |
| 2. Give examples of interaction features in finance. | |
| 3. Give examples of interaction features in medicine. | |
| 4. Give examples of interaction features in retail. | |
| 5. Give examples of interaction features in HR. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Interaction feature | Captures the **combined effect** of two variables that cannot be explained by either alone. |
| 2. Finance examples | **Debt-to-Income** = Debt / Income (affordability ratio). **Credit Utilization** = Balance / Credit Limit. |
| 3. Medicine examples | **Drug dose per kg** = dose / weight. **BMI** = weight / height². |
| 4. Retail examples | **Effective price** = price × (1 − discount). **Conversion rate** = conversions / impressions. |
| 5. HR examples | **Pay per year of experience** = salary / experience. **Performance per tenure** = rating / years. |

</details>

---

## Exercise FE-9: Text Feature Engineering

| Question | Your Answer |
|----------|-------------|
| 1. What are the three text feature approaches? | |
| 2. How does Bag-of-Words work? Pros and cons? | |
| 3. How does TF-IDF work? What does it do? | |
| 4. What are embeddings? Give examples. | |
| 5. Which approach is best for document classification? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Three text approaches | **Bag-of-Words/Count** (word counts). **TF-IDF** (term frequency × inverse document frequency). **Embeddings** (dense vectors of meaning). |
| 2. Bag-of-Words | Count occurrences of each word. **Pros**: simple, fast, interpretable. **Cons**: no word order, ignores meaning. |
| 3. TF-IDF | **Term Frequency × Inverse Document Frequency**. Downweights common words (the, a, is) and rewards rare but informative ones. **Best for**: document classification, search ranking. Handles corpus-wide word importance. |
| 4. Embeddings | Dense vector of meaning. Semantically similar words have similar vectors. **Examples**: Word2Vec, GloVe, FastText (handles subword morphology), BERT/sentence-transformers (state of the art). **Best for**: deep learning, semantic search. |
| 5. Best for document classification | **TF-IDF** is the standard baseline for document classification. Often works well with linear classifiers like Logistic Regression. |

</details>

---

## Exercise FE-10: Aggregation Features

| Question | Your Answer |
|----------|-------------|
| 1. What are aggregation features? | |
| 2. What is the leakage warning for aggregations? | |
| 3. How do you compute group-level aggregates? | |
| 4. What is a "relative feature"? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Aggregation features | **Group-level statistics** per entity (customer, product, store). Examples: total_spend, avg_spend, num_purchases, unique_categories. Encode an entity's context relative to peers. |
| 2. Leakage warning | Compute group stats on **training rows only**. Use group-hold or time-based splits to prevent test-set information leaking into aggregates. |
| 3. Compute group-level aggregates | `customer_stats = df.groupby("customer_id").agg(total_spend=("amount","sum"), avg_spend=("amount","mean"), num_purchases=("amount","count"), unique_cats=("product_category","nunique")).reset_index()` |
| 4. Relative feature | Individual value divided by group-level statistic: `spend_vs_cust_avg = amount / avg_spend`. Encodes "how does this individual compare to their group?" |

</details>

---

## Exercise FE-11: Domain-Specific Feature Examples

| Question | Your Answer |
|----------|-------------|
| 1. Finance/Credit domain features | |
| 2. Geospatial/Logistics domain features | |
| 3. E-Commerce/Retail domain features | |
| 4. Human Resources domain features | |
| 5. Healthcare domain features | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Finance/Credit | Debt-to-Income (DTI), Credit utilization ratio, Months since last delinquency, Number of hard inquiries (last 6M), Payment-to-balance ratio. |
| 2. Geospatial/Logistics | Haversine distance to store, Population density at zip code, Drive-time vs straight-line distance, Nearest competitor distance, Urban/suburban/rural classification. |
| 3. E-Commerce/Retail | Recency-Frequency-Monetary (RFM), Days since last purchase, Cart abandonment count, Category diversity score, Price sensitivity quartile. |
| 4. Human Resources | Tenure in current role, Promotions per year, Manager span of control, Salary vs band midpoint, Peer rating trajectory. |
| 5. Healthcare | Charlson Comorbidity Index, eGFR (kidney function score), BMI, waist-to-hip ratio, Medication adherence rate, Lab result trend (slope). |

</details>

---

## Exercise FE-12: Feature Selection Methods

| Question | Your Answer |
|----------|-------------|
| 1. Why does feature selection matter? | |
| 2. What are Filter methods? Pros/cons? | |
| 3. What are Wrapper methods? Pros/cons? | |
| 4. What are Embedded methods? Pros/cons? | |
| 5. Which method is Lasso (L1) regularization? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why feature selection matters | More features does not mean a better model. Irrelevant and redundant features: add noise, increase overfitting risk, slow training, cause multicollinearity, and suffer from curse of dimensionality. |
| 2. Filter methods | Score each feature independently using statistics (correlation, chi², mutual info, ANOVA F-test). **Pros**: fast, model-agnostic. **Cons**: blind to feature interactions. |
| 3. Wrapper methods | Try subsets of features and measure model performance (RFE, forward/backward selection). **Pros**: accurate — considers interactions. **Cons**: slow, risk of overfitting the selector. |
| 4. Embedded methods | Feature selection built into model training (Lasso L1 penalty, tree feature importance). **Pros**: fast and accurate. **Cons**: model-specific. |
| 5. Lasso | **Embedded method** — L1 regularization performs feature selection during training. |

</details>

---

## Exercise FE-13: Feature Evaluation Checklist

| Question | Your Answer |
|----------|-------------|
| 1. Predictive Power — how to evaluate? | |
| 2. No Leakage — what to check? | |
| 3. Stable at Serve — what to check? | |
| 4. Distribution Stable — what to check? | |
| 5. Business Sensible — why important? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Predictive Power | Measure **AUC/RMSE with and without** the feature. If gain < 0.001 AUC, question if it's worth the added complexity. |
| 2. No Leakage | Does it use information **unavailable at prediction time**? Example: 'total_spend' in a churn model could include post-churn spending. |
| 3. Stable at Serve | Can this feature be computed at **inference time** in production? Features needing full database scans may be impractical. |
| 4. Distribution Stable | Monitor with **PSI (Population Stability Index)**. Does the distribution shift significantly between train/test/prod? |
| 5. Business Sensible | Does adding this feature make logical sense? A feature that works but can't be explained erodes stakeholder trust in the model. |

</details>

---

## Exercise FE-14: Feature Engineering in Production

| Question | Your Answer |
|----------|-------------|
| 1. Why use sklearn Pipelines? | |
| 2. What is PSI and why monitor it? | |
| 3. What is the key rule for fitting vs transforming? | |
| 4. Why document features? | |
| 5. What is a Feature Store? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why use Pipelines | All transformations inside a Pipeline object ensure **identical processing at train and serve time**. Never transform outside the pipeline. |
| 2. PSI monitoring | **Population Stability Index** tracks feature distribution drift. Silent drift — same feature, shifted distribution — causes invisible model decay. Monitor in production. |
| 3. Key rule | **fit()** only on training data. **transform()** on validation and test. Fitting on all data causes leakage — the most common ML mistake. |
| 4. Document features | For each feature record: definition, source column(s), business logic, known issues, and date added. "What features did v2.3 use?" should always be answerable. |
| 5. Feature Store | For large-scale production: pre-compute and cache features. Avoid recomputing at every inference request. |

</details>

---

## Exercise FE-15: Feature Engineering Checklist

| Category | Your Answer (check off) |
|----------|--------------------------|
| Understand the Data | ☐ |
| Numerical Transformations | ☐ |
| Categorical / Text | ☐ |
| Aggregations | ☐ |
| Temporal | ☐ |
| Selection & Pipeline | ☐ |

<details>
<summary>📖 Click for Answers</summary>

**Complete Checklist:**

**Understand the Data:**
- ☐ Read data dictionary & talk to domain experts
- ☐ EDA: distributions, correlations, missingness
- ☐ Identify target leakage risks upfront

**Numerical Transformations:**
- ☐ Log/power transform skewed features
- ☐ Scale (StandardScaler for most, MinMax for NNs)
- ☐ Create polynomial & ratio features

**Categorical / Text:**
- ☐ Encode: OHE (nominal), ordinal, target (high-card)
- ☐ TF-IDF or embeddings for text columns
- ☐ Add sentiment, keyword flags, text length

**Aggregations:**
- ☐ Group-level stats per entity (customer, product)
- ☐ Relative features: individual vs. group mean
- ☐ Compute on train only — no leakage

**Temporal:**
- ☐ Extract hour, day, month, quarter, is_weekend
- ☐ Cyclical encode periodic features (sin/cos)
- ☐ Add lag and rolling mean/std if time series

**Selection & Pipeline:**
- ☐ Remove zero-variance & highly correlated features
- ☐ Use SHAP/MI for importance ranking
- ☐ Wrap everything in sklearn Pipeline

</details>

---

# SECTION 3: DATA VISUALIZATION (3.3 Data Visualization)

---

## Exercise DV-1: Why Visualize Data?

| Question | Your Answer |
|----------|-------------|
| 1. What does Anscombe's Quartet demonstrate? | |
| 2. What is the 60,000× faster statistic? | |
| 3. List the 6 reasons to visualize before modeling. | |
| 4. What is the EDA Visualization Workflow? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Anscombe's Quartet | Four datasets with **IDENTICAL summary statistics** (mean(x)=9, mean(y)=7.5, var(x)=11, var(y)≈4.12, correlation=0.816, regression line: y=3+0.5x) — yet they look completely different when plotted. **Visualization catches what numbers hide.** |
| 2. 60,000× faster | Humans process visual information **60,000× faster** than plain text. |
| 3. Six reasons | **1. Understand Distributions**: see shape, skew, bimodality. **2. Spot Outliers**: jump out visually in under a second. **3. Find Relationships**: scatter plots reveal correlation, clusters, non-linear patterns. **4. Check Data Quality**: missing patterns, wrong values, duplicates. **5. Communicate Insights**: stakeholders understand charts, not tables. **6. Guide Feature Engineering**: what to log-transform, bin, or combine becomes obvious. |
| 4. EDA Visualization Workflow | **Step 1**: Profile (df.info(), df.describe()). **Step 2**: Distributions (histograms). **Step 3**: Target Var. **Step 4**: Relationships (scatter plots, correlation matrix). **Step 5**: By-Group (compare across categories). **Step 6**: Document (record all findings before modeling). |

</details>

---

## Exercise DV-2: Tufte's Data-Ink Ratio

| Question | Your Answer |
|----------|-------------|
| 1. What is the Data-Ink Ratio? | |
| 2. Who introduced the Data-Ink Ratio? | |
| 3. List 6 things to keep (maximize data ink). | |
| 4. List 8 types of chartjunk to remove. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Data-Ink Ratio | **Data-Ink Ratio = Ink used to display data / Total ink used in the graphic.** "Above all else show the data." — Edward Tufte. |
| 2. Who introduced it | **Edward Tufte** in "The Visual Display of Quantitative Information" (1983). |
| 3. What to keep (maximize data ink) | ✓ Only necessary gridlines (horizontal only, light grey). ✓ Direct labels instead of legend. ✓ Remove top/right axis spines. ✓ Thin axis lines. ✓ White/transparent plot background. ✓ Proportional font sizes. ✓ Color only to encode information. ✓ Sufficient whitespace. |
| 4. Chartjunk to remove | ✗ Heavy border around plot. ✗ Background fill or gradient. ✗ Gridlines on every axis tick. ✗ 3D effects on 2D data. ✗ Unnecessary legend (1 series). ✗ Decorative icons or clip art. ✗ Redundant tick labels. ✗ Shadows on bars. ✗ Font sizes all the same weight. |

</details>

---

## Exercise DV-3: Gestalt Principles

| Question | Your Answer |
|----------|-------------|
| 1. What is Proximity? | |
| 2. What is Continuity? | |
| 3. What is Similarity? | |
| 4. What is Closure? | |
| 5. What is Enclosure? | |
| 6. What is Figure/Ground? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Proximity | Elements placed **close together appear related**. Group related chart elements closely; separate groups with whitespace. |
| 2. Continuity | Eyes follow **smooth lines and curves**. Line charts exploit this — the eye connects points into trends naturally. |
| 3. Similarity | Elements with the **same color, shape, or size** look like they belong together. Use consistent color for consistent category. |
| 4. Closure | The brain **completes incomplete shapes**. Dot plots with a reference line still feel "connected" without explicitly drawing it. |
| 5. Enclosure | Elements surrounded by a **border or box appear grouped**. Use panel backgrounds in faceted charts to separate sub-plots. |
| 6. Figure/Ground | The **main element stands out from its background**. Use strong contrast for the key data series; mute everything else. |

</details>

---

## Exercise DV-4: Color in Data Visualization

| Question | Your Answer |
|----------|-------------|
| 1. What is Sequential colormap? When to use? | |
| 2. What is Diverging colormap? When to use? | |
| 3. What is Qualitative colormap? When to use? | |
| 4. What percentage of men and women are colorblind? | |
| 5. What color pairs should be avoided? | |
| 6. Name colorblind-safe palettes. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Sequential | Ordered, numeric data (Blues palette). **Use for**: low to high counts, income, density. |
| 2. Diverging | Meaningful midpoint (RdYlBu palette). **Use for**: correlation (-1 to 1), temperature anomaly, sentiment. |
| 3. Qualitative | Nominal categories (tab10/matplotlib default). **Use for**: department, country, species (no order). |
| 4. Colorblind prevalence | **8% of men**, **0.5% of women** are colorblind. |
| 5. Avoid these pairs | ✗ Red + Green (most common CVD). ✗ Green + Brown. ✗ Blue + Purple. ✗ Light Green + Yellow. |
| 6. Colorblind-safe palettes | ✓ Viridis, ✓ Cividis, ✓ ColorBrewer palettes, ✓ IBM Carbon color-safe palette, ✓ Wong 2011 8-color scientific palette. |

</details>

---

## Exercise DV-5: Chart Types — When to Use

| Question | Your Answer |
|----------|-------------|
| 1. Compare values across categories → best chart | |
| 2. Trend over time → best chart | |
| 3. Relationship between 2 numeric variables → best chart | |
| 4. Distribution of one numeric variable → best chart | |
| 5. Spread, median, outliers per group → best chart | |
| 6. Correlation between many features → best chart | |
| 7. Part-to-whole proportions → best chart | |
| 8. High-dimensional data overview → best chart | |
| 9. Data across geography → best chart | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Compare values across categories | **Bar chart** (vertical or horizontal) — alternative: Dot plot |
| 2. Trend over time | **Line chart** — alternative: Area chart |
| 3. Relationship between 2 numeric variables | **Scatter plot** — alternative: Bubble chart |
| 4. Distribution of one numeric variable | **Histogram + KDE** — alternative: Box plot, violin plot |
| 5. Spread, median, outliers per group | **Box plot** — alternative: Violin plot |
| 6. Correlation between many features | **Heatmap** (correlation matrix) — alternative: Pair plot |
| 7. Part-to-whole proportions | **Bar chart** (stacked) — alternative: Pie/donut (5 or fewer slices) |
| 8. High-dimensional data overview | **Pair plot** (sns.pairplot) — alternative: PCA plot, UMAP |
| 9. Data across geography | **Choropleth map** — alternative: Bubble map |

</details>

---

## Exercise DV-6: Bar Chart Best Practices

| Question | Your Answer |
|----------|-------------|
| 1. When to use bar charts? | |
| 2. What are common mistakes with bar charts? | |
| 3. Why should bars be sorted? | |
| 4. What is the rule for y-axis starting point? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. When to use | Compare values across distinct categories. Show counts, totals, averages per group. Grouped bar: compare multiple groups side by side. Stacked bar: part-to-whole composition. |
| 2. Common mistakes | ✗ Y-axis not starting at zero (truncated axes mislead). ✗ Too many categories (>12) → switch to horizontal. ✗ 3D bars — never use. ✗ Replacing with a pie chart — bar charts are almost always better. ✗ Missing axis labels or units. ✗ Bars sorted randomly — always sort by value. |
| 3. Why sort bars | **Always sort by value** — makes comparison easier for the viewer. Unsorted bars hide the ranking. |
| 4. Y-axis rule | **Bar charts must always start at zero** — truncated y-axis exaggerates differences. |

</details>

---

## Exercise DV-7: Visualization Anti-Patterns

| Question | Your Answer |
|----------|-------------|
| 1. Truncated Y-axis — problem and fix | |
| 2. 3D Charts — problem and fix | |
| 3. Chartjunk — problem and fix | |
| 4. Too many colors — problem and fix | |
| 5. Wrong chart type — problem and fix | |
| 6. Missing context — problem and fix | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Truncated Y-axis | **Problem**: Starting y-axis at non-zero exaggerates differences (5% change looks like 500%). **Fix**: Start at zero for bar charts. For line charts, add visible break symbol + annotation. |
| 2. 3D Charts | **Problem**: 3D perspective distorts bar heights and pie slices; front slices appear larger. **Fix**: Use 2D always. Never use 3D pie, 3D bar, or 3D surface. |
| 3. Chartjunk | **Problem**: Heavy gridlines, gradients, shadows, clip art, 3D effects — all visual noise. **Fix**: Remove everything that is not data or necessary axis/label context. |
| 4. Too many colors | **Problem**: 15 colors in a pie, 10 lines on one chart — impossible to distinguish. **Fix**: Maximum 5–7 categorical colors. Highlight one series; grey out the rest. |
| 5. Wrong chart type | **Problem**: Pie with 12 slices, line chart for unordered categories, bar chart for distribution. **Fix**: Match chart to data type and relationship. Use decision guide. |
| 6. Missing context | **Problem**: No title, no axis labels, no units, no source — reader can't interpret chart. **Fix**: Every chart must have: title (the insight), x-label+units, y-label+units, and data source. |

</details>

---

## Exercise DV-8: Storytelling & Dashboard Design

| Question | Your Answer |
|----------|-------------|
| 1. What are the 4 components of storytelling with data? | |
| 2. What is the layout hierarchy for dashboards? | |
| 3. What should KPI cards include? | |
| 4. What context information should dashboards display? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Four components | **1. Context**: Who + Why (audience, decision, what they know). **2. Conflict**: The question (one insight the chart must communicate). **3. Resolution**: The answer (design so answer is obvious within 5 seconds). **4. Action**: The next step (what the audience should do next). |
| 2. Layout hierarchy | **Top-left**: most important KPI (prime real estate). **Flow**: left to right, top to bottom (reading direction). **Group**: related charts visually with whitespace. **1–2 key numbers** per section maximum. |
| 3. KPI cards | Large, bold numbers for key metrics — instantly scannable. Color coding: red=bad, green=good (with accessibility care). Include trend direction and delta from previous period. |
| 4. Context information | ✓ Always show date range of data. ✓ Include last-updated timestamp. ✓ Display data source clearly. ✓ State clearly when filters are active. ✓ Add sparkline for time context when space allows. |

</details>

---

## Exercise DV-9: Interactive vs Static Visualization

| Question | Your Answer |
|----------|-------------|
| 1. When is interactive visualization worth it? | |
| 2. What are the popular interactive libraries? | |
| 3. When is static visualization better? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. When interactive is worth it | ✓ Exploratory analysis — let analysts drill into data. ✓ Dashboards — viewers need to filter and slice. ✓ Stakeholder demos — invite engagement and questions. ✓ Complex datasets with many dimensions to expose. |
| 2. Popular libraries | **Plotly** — full-featured interactive charts; integrates with Dash. **Bokeh** — web-ready charts; great for streaming data. **D3.js** — maximum flexibility; steep learning curve. **Altair** — declarative grammar of graphics; clean syntax. |
| 3. When static is better | ✗ Published papers and academic reports — control the message. ✗ Print materials — no renderer available. ✗ Presentations — guide the audience to your conclusion. ✗ Accessibility-critical contexts — static is more reliable. |

</details>

---

## Exercise DV-10: Geospatial Visualization

| Question | Your Answer |
|----------|-------------|
| 1. What is a Choropleth map? When to use? | |
| 2. What is a Bubble map? When to use? | |
| 3. What is a Heatmap/Density map? When to use? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Choropleth map | Color-fill regions by value. **Use for**: Country/state/region-level data. One value per region (rate, count, score). Sequential or diverging color palette. `folium.Choropleth()` / `plotly.choropleth()`. |
| 2. Bubble map | Points on map sized by value. **Use for**: City-level data, store locations, event hotspots. Point-level data with magnitude to encode. Overlapping bubbles acceptable (use alpha). Color + size encodes two dimensions. `plotly.scatter_geo(size=col)`. |
| 3. Heatmap/Density | Kernel density estimation on a map. **Use for**: Thousands of lat/lng points too many to show individually. Reveal hot spots without cluttering. No clear region boundaries available. `folium.plugins.HeatMap(data)`. |

</details>

---

# 📊 COMPLETE COVERAGE SUMMARY

| Category | Concepts | Status |
|----------|----------|--------|
| Data Preparation | All major concepts | ✅ 100% |
| Feature Engineering | All major concepts | ✅ 100% |
| Data Visualization | All major concepts | ✅ 100% |
| **TOTAL** | **All Week 3 concepts** | ✅ **100%** |

---

## 📝 How to Use This Document

1. **Read the question**, write your answer in the blank/box
2. **Click the dropdown** to reveal the model answer
3. **Compare** your answer to the model
4. **Re-study** any sections where you got something wrong
5. **Mark** your confidence level for each topic

---

**Good luck with your exam! 🎯**