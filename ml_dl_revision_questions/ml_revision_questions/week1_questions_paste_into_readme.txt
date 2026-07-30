# 📚 WEEK 1 — COMPLETE STUDY GUIDE
## All Exercises with Answers in Spoiler Format

---

# SECTION 1: WARM-UP

---

## Exercise 2: "Traditional vs. ML" Decision Tree

For each scenario, write **"Traditional Code"** or **"Machine Learning"** and **why**:

| Scenario | Your Answer | Why? |
|----------|-------------|------|
| Sort 1 million numbers | | |
| Detect credit card fraud | | |
| Convert Celsius to Fahrenheit | | |
| Predict if a customer will churn | | |
| Identify objects in a photo | | |
| Calculate a mortgage payment | | |
| Transcribe speech to text | | |
| Recommend products to a user | | |

<details>
<summary>📖 Click for Answers</summary>

| Scenario | Answer | Why? |
|----------|--------|------|
| Sort 1 million numbers | **Traditional Code** | Perfect rules exist (quicksort, mergesort). Deterministic, no ambiguity. ML adds no value. |
| Detect credit card fraud | **Machine Learning** | Fraud patterns are complex, evolving, and subtle. Can't write explicit rules for all cases. |
| Convert Celsius to Fahrenheit | **Traditional Code** | Exact mathematical formula: `°F = °C × 9/5 + 32`. Deterministic and perfect. |
| Predict if a customer will churn | **Machine Learning** | Complex behavioral signals. No simple rule exists. Patterns are learned from data. |
| Identify objects in a photo | **Machine Learning** | 150,000+ pixel values. Can't enumerate rules for all objects, lighting, angles, variations. |
| Calculate a mortgage payment | **Traditional Code** | Formula is deterministic and exact (principal, interest rate, term). |
| Transcribe speech to text | **Machine Learning** | Infinite variation in accent, tone, noise. Can't write rules for all pronunciations. |
| Recommend products to a user | **Machine Learning** | Complex preference patterns. Collaborative/content-based filtering learned from data. |

</details>

---

## Exercise 3: Paradigm Matching

Match each problem to: **Supervised / Unsupervised / Reinforcement Learning**

| Problem | Paradigm |
|---------|----------|
| Group customers by purchasing behavior | |
| Teach a robot to walk | |
| Predict house prices from features | |
| Find topics in a collection of news articles | |
| Detect spam emails | |
| Train an agent to play chess | |
| Segment images by similar visual features | |
| Predict tomorrow's temperature | |
| Identify anomalies in network traffic | |
| Optimize a supply chain with delayed rewards | |

<details>
<summary>📖 Click for Answers</summary>

| Problem | Paradigm |
|---------|----------|
| Group customers by purchasing behavior | **Unsupervised** (Clustering) |
| Teach a robot to walk | **Reinforcement Learning** (Trial and error with rewards) |
| Predict house prices from features | **Supervised** (Regression) |
| Find topics in a collection of news articles | **Unsupervised** (Topic modeling) |
| Detect spam emails | **Supervised** (Classification) |
| Train an agent to play chess | **Reinforcement Learning** (Rewards for winning) |
| Segment images by similar visual features | **Unsupervised** (Clustering) |
| Predict tomorrow's temperature | **Supervised** (Regression) |
| Identify anomalies in network traffic | **Unsupervised** (Anomaly detection) |
| Optimize a supply chain with delayed rewards | **Reinforcement Learning** (Sequential decisions) |

</details>

---

# SECTION 2: CORE TOPICS

---

## Exercise 4: "Spot the Leakage"

Which of these is **data leakage**? (Write YES/NO and explain why)

| Practice | Leakage? | Why/Why not? |
|----------|----------|--------------|
| A. Scaling features using mean/std from the full dataset *before* splitting | | |
| B. Shuffling time-series data randomly | | |
| C. Using cross-validation to tune hyperparameters | | |
| D. Having duplicate rows across train and test sets | | |
| E. Training on 80%, validating on 20% | | |
| F. Encoding categorical variables using global statistics before splitting | | |
| G. Using future data as a feature for predicting the past | | |
| H. Removing outliers based on statistics from the full dataset | | |
| I. Using test set performance to decide when to stop training | | |

<details>
<summary>📖 Click for Answers</summary>

| Practice | Leakage? | Why/Why not? |
|----------|----------|--------------|
| A. Scaling features using mean/std from the full dataset *before* splitting | **YES** | Test set information leaks into training. Should fit scaler on TRAIN only, then transform both. |
| B. Shuffling time-series data randomly | **YES** | Future data leaks into past. Temporal data must be split chronologically. |
| C. Using cross-validation to tune hyperparameters | **NO** | Proper use of validation. CV uses only training folds, test set remains untouched. |
| D. Having duplicate rows across train and test sets | **YES** | Model effectively sees test data during training. Must deduplicate before splitting. |
| E. Training on 80%, validating on 20% | **NO** | Standard holdout validation. Test set untouched. |
| F. Encoding categorical variables using global statistics before splitting | **YES** | Statistics like frequency/mean from full dataset leak test info. Fit encoder on train only. |
| G. Using future data as a feature for predicting the past | **YES** | Classic temporal leakage. Features must come from the same time as training data. |
| H. Removing outliers based on statistics from the full dataset | **YES** | Outlier thresholds from full dataset leak test info. Fit on train only. |
| I. Using test set performance to decide when to stop training | **YES** | Test set should NEVER be used for any decision. Use validation set for early stopping. |

</details>

---

## Exercise 5: Metrics Scenario (Cancer Screening)

You're building a **cancer screening model**. Dataset: 99% healthy, 1% sick.

| Question | Your Answer |
|----------|-------------|
| What metric would be **misleading** if used alone? Why? | |
| What metric should you **prioritize**? Why? | |
| What would a "dumb" model that always predicts "healthy" score on **accuracy**? | |
| What would it score on **recall**? | |
| What would it score on **precision**? | |
| What F1 score would the "dumb" model have? | |
| What would AUC-ROC be for the "dumb" model? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| What metric would be **misleading** if used alone? Why? | **Accuracy**. 99% accuracy is trivial (always predict "healthy"). It hides that we catch 0% of sick patients. |
| What metric should you **prioritize**? Why? | **Recall (Sensitivity)**. Missing a cancer patient (False Negative) is life-threatening. We need to catch as many sick patients as possible. |
| What would a "dumb" model that always predicts "healthy" score on **accuracy**? | **99%** (9,900 healthy correct / 10,000 total) |
| What would it score on **recall**? | **0%** (0 sick caught / 100 sick total) |
| What would it score on **precision**? | **Undefined (0/0)** because it predicts no positives. |
| What F1 score would the "dumb" model have? | **0** (harmonic mean of 0 and undefined is 0) |
| What would AUC-ROC be for the "dumb" model? | **0.5** (random guessing — model never changes threshold, TPR=0 at all FPR values) |

</details>

---

## Exercise A: "Fix the Broken Workflow"

**Scenario:** A data scientist does this:
1. Splits data into Train (70%) / Test (30%)
2. Scales all features using the **entire dataset's** mean/std
3. Trains a KNN model on Train
4. Tunes K by testing values on Test and picking the best
5. Reports final Test accuracy as "true generalization"

**Your task:** List **every mistake** and explain the correct approach:

| Mistake | Correct Approach |
|---------|-------------------|
| 1. | |
| 2. | |
| 3. | |
| 4. | |
| 5. | |

<details>
<summary>📖 Click for Answers</summary>

| Mistake | Correct Approach |
|---------|-------------------|
| 1. Scaling features using **entire dataset** mean/std | Fit scaler on **TRAINING SET ONLY**. Transform train, then use same transform on validation/test. |
| 2. Not splitting into **validation set** | Use **three-way split**: Train (60%) → tune on Validation (20%) → evaluate on Test (20%). |
| 3. Tuning K by testing on **Test** set | Use **Validation set** or **Cross-Validation** to tune hyperparameters. Test is for final evaluation ONLY. |
| 4. Looking at Test set multiple times | **Test set is used ONCE** at the very end. If you tune based on test, your final estimate is biased. |
| 5. Reporting Test accuracy as "generalization" | **Test accuracy is the final estimate** — but ONLY if test was never used before. Report with confidence intervals. |

**Correct Workflow:**
```
All Data → Split → Train Set (fit model) → Val Set (tune hyperparameters) → Test Set (final evaluate ONCE)
```

</details>

---

## Exercise B: "Underfitting vs. Overfitting Diagnosis"

For each scenario, diagnose as **Underfitting** or **Overfitting** and suggest a fix:

| Scenario | Diagnosis | What would you do to fix it? |
|----------|-----------|------------------------------|
| Train error: 2%, Validation error: 25% | | |
| Train error: 40%, Validation error: 42% | | |
| K=1 on KNN: perfect on Train, terrible on Test | | |
| K=100 on KNN: 60% on both Train and Test | | |
| Learning curves: both converge to high error | | |
| Learning curves: training error low, validation error high, gap widening | | |
| Training error: 15%, Validation error: 16% (both acceptable) | | |
| Training error: 0%, Validation error: 30% | | |

<details>
<summary>📖 Click for Answers</summary>

| Scenario | Diagnosis | Fix |
|----------|-----------|-----|
| Train error: 2%, Validation error: 25% | **Overfitting** (High Variance) | Get more data, simpler model, add regularization, feature selection, early stopping |
| Train error: 40%, Validation error: 42% | **Underfitting** (High Bias) | Use more complex model, add features, reduce regularization, train longer |
| K=1 on KNN: perfect on Train, terrible on Test | **Overfitting** | Increase K to smooth decision boundary |
| K=100 on KNN: 60% on both Train and Test | **Underfitting** | Decrease K (too many neighbors smooths away patterns) |
| Learning curves: both converge to high error | **Underfitting** | Need better model architecture or more informative features |
| Learning curves: training error low, validation error high, gap widening | **Overfitting** | More data will help close the gap, or add regularization |
| Training error: 15%, Validation error: 16% (both acceptable) | **Good Fit** | Model generalizes well. No action needed. |
| Training error: 0%, Validation error: 30% | **Severe Overfitting** | Model memorized training data. Use regularization, simpler model, more data. |

</details>

---

## Exercise C: "Metric Translation"

Translate business requirements into ML metrics:

| Business Requirement | Best Metric(s) | Why? |
|----------------------|----------------|------|
| "We must not miss any fraud transactions — every missed one costs $10,000" | | |
| "We can't afford to annoy customers by marking real emails as spam" | | |
| "We need a balanced measure when classes are unequal" | | |
| "We want to compare models without picking a threshold" | | |
| "We're predicting house prices and want errors in dollars" | | |
| "We need to explain to executives what % of variance our model explains" | | |
| "We're forecasting sales and stakeholders understand percentages best" | | |
| "We need a model that balances catching fraud with not falsely accusing customers" | | |
| "We're comparing models across multiple classes with different frequencies" | | |

<details>
<summary>📖 Click for Answers</summary>

| Business Requirement | Best Metric(s) | Why? |
|----------------------|----------------|------|
| "We must not miss any fraud transactions" | **Recall** | Minimize False Negatives. Every missed fraud costs money. |
| "We can't afford to mark real emails as spam" | **Precision** | Minimize False Positives. Real emails in spam annoy customers. |
| "Balanced measure when classes are unequal" | **F1 Score** | Harmonic mean balances precision and recall. Handles imbalance well. |
| "Compare models without picking a threshold" | **AUC-ROC** | Threshold-independent. Measures ranking ability across all thresholds. |
| "Predicting house prices — errors in dollars" | **RMSE** (or MAE) | Same units as target. RMSE penalizes large errors more heavily. |
| "Explain % of variance explained" | **R²** | Proportion of variance explained by the model. Intuitive for stakeholders. |
| "Stakeholders understand percentages best" | **MAPE** | Mean Absolute Percentage Error. Intuitive for business reporting. |
| "Balance catching fraud vs false accusations" | **F1 Score** | Balances precision and recall. Optimizes both simultaneously. |
| "Comparing models across multiple classes with different frequencies" | **Weighted Average** | Accounts for class imbalance by weighting by class support. |

</details>

---

## Exercise D: "Ethics & Pitfalls Scenario"

**Scenario:** A bank builds an ML model to approve loans. They train on historical data (2000–2020). The model achieves 94% accuracy. They deploy it.

| Question | Your Answer |
|----------|-------------|
| 1. What pitfall might occur if the economy changes after 2020? What's this called? | |
| 2. If the historical data contains biased decisions against certain groups, what problem emerges? | |
| 3. The bank wants to understand *why* a customer was denied. What concept from your slides applies? | |
| 4. Who is responsible if the model discriminates? | |
| 5. What's one way to detect bias before deployment? | |
| 6. What privacy risk might exist with ML models? | |
| 7. How would you fix overfitting in this model? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What pitfall might occur if the economy changes after 2020? What's this called? | **Distribution Shift** (or Concept Drift). The data distribution changed after COVID, making the model outdated. |
| 2. If the historical data contains biased decisions against certain groups, what problem emerges? | **Biased Training Data**. The model inherits and amplifies historical discrimination. Fairness violation. |
| 3. The bank wants to understand *why* a customer was denied. What concept applies? | **Explainability** (or Interpretability). Need to understand model decisions, especially in high-stakes domains. |
| 4. Who is responsible if the model discriminates? | **Accountability**. The company, data scientists, and decision-makers share responsibility. Legal frameworks are still evolving. |
| 5. What's one way to detect bias before deployment? | **Audit data sources** and use **fairness metrics** (e.g., demographic parity, equal opportunity) on validation data. |
| 6. What privacy risk might exist with ML models? | Models can **memorize training data** (e.g., medical records). Predictions might inadvertently leak patient information. |
| 7. How would you fix overfitting in this model? | More data, cross-validation, regularization, simpler model, feature selection, or early stopping. |

</details>

---

# SECTION 3: DEEP APPLICATION

---

## Exercise E: "The Model Selection Memo"

**Scenario:** Your company wants to build a system that:
- Detects defective products on an assembly line from camera images
- Has 50,000 labeled images (10% defective, 90% good)
- Needs to explain decisions to quality control auditors
- Must process 1,000 images per second
- Cannot miss defective products (costs $1,000 per miss)
- False alarms cost $50 each (slows down the line)

**Your task:** Write a **1-page memo** (bullet points fine) addressing:

| Question | Your Answer |
|----------|-------------|
| 1. Is this ML or Traditional Software? Why? | |
| 2. Which paradigm (Supervised/Unsupervised/RL)? Why? | |
| 3. How would you split the data? Any special considerations? | |
| 4. Which metric(s) would you prioritize? Why? | |
| 5. What validation strategy would you use? Why? | |
| 6. What's one ethical/pitfall concern you'd flag? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Is this ML or Traditional Software? Why? | **Machine Learning**. Can't write explicit rules for detecting all possible defects in images (lighting, angle, defect types vary infinitely). |
| 2. Which paradigm? Why? | **Supervised Learning** (Classification). We have labeled images (defective/good). Need to map images → binary classification. |
| 3. How would you split the data? Any special considerations? | **Stratified Split** (70/15/15 or 60/20/20) to preserve 10% defect rate in all splits. Also **Group Split** if multiple images of same product exist to prevent leakage. |
| 4. Which metric(s) would you prioritize? Why? | **Recall** (must catch defects — FN costs $1,000) AND **Precision** (FP costs $50 and slows line). Use **F1 Score** to balance both. Also report **FPR** (false positive rate) for business context. |
| 5. What validation strategy would you use? Why? | **Stratified K-Fold** (K=5 or 10) for reliable performance estimate with limited data. Ensures each fold has the same 10% defect ratio. |
| 6. What's one ethical/pitfall concern you'd flag? | **Explainability** — auditors need to understand why products were rejected. Use interpretable models (e.g., decision trees) or post-hoc explainability tools (SHAP/LIME). Also monitor for **distribution shift** as the assembly line changes over time. |

</details>

---

## Exercise F: "Design the Experiment"

**Scenario:** You have a tiny dataset of **200 medical records** (100 sick, 100 healthy). You need to compare:
- KNN (with different K values: 1, 3, 5, 7, 11, 15)
- Logistic Regression

| Question | Your Answer |
|----------|-------------|
| 1. What split strategy would you use? (Holdout? K-Fold? Which K?) Justify. | |
| 2. If you use K-Fold, do you need stratified? Why/why not? | |
| 3. How would you choose the best K for KNN? | |
| 4. How would you compare the two models fairly? | |
| 5. How do you get a final, unbiased performance estimate? | |
| 6. What metric would you report? (Remember: balanced dataset here) | |
| 7. What K would you NOT use for cross-validation here and why? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What split strategy would you use? Justify. | **K-Fold Cross-Validation** (K=5 or 10). With only 200 samples, holdout (80/20) wastes data (only 160 train). 5-fold uses 160 train per fold; 10-fold uses 180 train per fold. |
| 2. If you use K-Fold, do you need stratified? Why? | **YES**. Need to ensure each fold has 50/50 sick/healthy split. Without stratification, some folds might have 40/60 or worse, making validation meaningless. |
| 3. How would you choose the best K for KNN? | Use **inner cross-validation** on the training folds. For each candidate K (1,3,5,7,11,15), compute average validation accuracy across folds and pick the K with highest average performance. |
| 4. How would you compare the two models fairly? | Use **nested cross-validation**. Outer loop: train both models on K-1 folds, validate on the held-out fold. Inner loop: tune K for KNN. Compare average performance across outer folds. |
| 5. How do you get a final, unbiased performance estimate? | After selecting the best model + hyperparameters via CV, train on **all training data** and evaluate **ONCE** on the held-out test set. Report that as final generalization error. |
| 6. What metric would you report? | **Accuracy** (balanced dataset) plus **Precision**, **Recall**, and **F1** for completeness. Since classes are balanced, accuracy is meaningful here. |
| 7. What K would you NOT use for cross-validation here and why? | **LOOCV (K=200)** — computationally expensive (200 training runs) and has high variance. With only 200 samples, 10-fold CV is sufficient. |

</details>

---

# SECTION 4: MASTERY & SYNTHESIS

---

## Exercise G: "The Deployment Disaster"

**Scenario:** A team deployed a model that:
- Achieved **99% accuracy** in testing
- **Fails catastrophically** in production (50% accuracy)

**Investigation reveals:**

| Mistake | What's it called? | Why did it cause optimistic results? | What should they have done instead? |
|---------|-------------------|--------------------------------------|--------------------------------------|
| Scaled features using full dataset before splitting | | | |
| Shuffled time-series data randomly | | | |
| Tuned hyperparameters on the test set | | | |
| Trained on 2010-2019, deployed in 2020 (COVID changed everything) | | | |
| Test set contained duplicate images from training | | | |
| Removed outliers using full dataset statistics | | | |

<details>
<summary>📖 Click for Answers</summary>

| Mistake | What's it called? | Why did it cause optimistic results? | What should they have done instead? |
|---------|-------------------|--------------------------------------|--------------------------------------|
| Scaled features using full dataset before splitting | **Data Leakage** | Test set mean/std leaked into training, making training artificially easier | Fit scaler on TRAIN only, transform train/val/test separately |
| Shuffled time-series data randomly | **Temporal Leakage** | Future data used to predict past. Model learned patterns that don't exist in real time | Split chronologically: train on older data, test on newer |
| Tuned hyperparameters on the test set | **Test Set Contamination** | Test set was used for decisions, so it became biased — no longer represents unseen data | Use validation set or CV for tuning. Test is for final evaluation ONLY |
| Trained on 2010-2019, deployed in 2020 (COVID changed everything) | **Distribution Shift** (Concept Drift) | Model learned patterns from pre-COVID world. These patterns changed fundamentally in 2020 | Monitor for drift in production and retrain regularly. Use more recent data for training |
| Test set contained duplicate images from training | **Data Leakage** | Model effectively saw test images during training. Performance was artificially inflated | Deduplicate data BEFORE splitting. Use Group Split if needed |
| Removed outliers using full dataset statistics | **Data Leakage** | Outlier thresholds from test data influenced training set composition | Fit outlier detection on TRAIN only; transform all data with train-derived thresholds |

</details>

---

## Exercise H: "Teach It to a Non-Technical Boss"

**Scenario:** Your boss (non-technical) asks:
> *"Why can't we just write rules for everything? Why do we need this 'machine learning' stuff? And how do we even know it works?"*

**Your task:** Write a **response** (max 300 words) that:
- Explains when ML beats rules (use examples from your slides)
- Explains how we know a model works (mention: train/val/test, metrics)
- Mentions **one risk** they should be aware of
- Uses **zero jargon** (no: bias-variance, overfitting, AUC-ROC, etc.)

<details>
<summary>📖 Click for Sample Answer</summary>

**Sample Response:**

"Rules work great when the logic is clear and stable — like calculating interest payments or sorting a list. But many problems are too complex for us to write rules by hand. Take fraud detection: fraudsters constantly change their tactics. There's no way to write rules for every possible scam. Instead, we show ML systems thousands of past examples (this was fraud, this was legitimate) and the system finds the subtle patterns itself. It adapts as fraud evolves.

For face recognition, how would you write rules for every angle, lighting condition, or expression? You can't. But with ML, we show it millions of faces and it learns what makes a face recognizable.

As for knowing if it works: we split our data. We hide a portion of the examples, train on the rest, and only test on the hidden data at the very end. We use metrics that matter: if we can't afford to miss fraud, we measure how many we catch. If false alarms cost us, we measure those too. We never let the model see the hidden test data during development — that way our final score is honest.

One risk: ML models learn from historical data. If that data contains past mistakes or biases, the model will inherit them. We need to actively check for this."

</details>

---

# SECTION 5: GAP FILLERS — HIGH PRIORITY

---

## Exercise I: "Scale or Die" — Feature Scaling for KNN

**Scenario:** You have a dataset with:
- Age: 25, 30, 35, 40, 45
- Salary: 50,000, 60,000, 70,000, 80,000, 90,000

| Question | Your Answer |
|----------|-------------|
| 1. If you use Euclidean distance without scaling, which feature dominates? Show the math for two points (Age 25/Salary 50k vs Age 30/Salary 60k). | |
| 2. Apply **Min-Max Normalization** to both features. Show your work. | |
| 3. Apply **Z-Score Standardization** to both features. Show your work. | |
| 4. Which scaling method is more robust to outliers? Why? | |
| 5. For KNN, is scaling always necessary? Why or why not? | |
| 6. What happens if you scale *after* splitting vs *before* splitting? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Which feature dominates? Show math. | **Salary dominates completely**. Distance = √((30-25)² + (60000-50000)²) = √(25 + 100,000,000) ≈ √100,000,025 ≈ 10,000. The age difference (25) is negligible compared to salary difference (10,000). |
| 2. Min-Max Normalization | Age: [25→0, 30→0.25, 35→0.5, 40→0.75, 45→1]; Salary: [50k→0, 60k→0.25, 70k→0.5, 80k→0.75, 90k→1]. Formula: (x - min)/(max - min) |
| 3. Z-Score Standardization | Mean Age=35, Std Age≈7.91; Mean Salary=70k, Std Salary≈15,811. Age: [25→-1.26, 30→-0.63, 35→0, 40→0.63, 45→1.26]; Salary: [50k→-1.26, 60k→-0.63, 70k→0, 80k→0.63, 90k→1.26]. Formula: (x - μ)/σ |
| 4. Which scaling method is more robust to outliers? | **Z-Score Standardization** — standard deviation is less sensitive to extreme outliers than min/max range. |
| 5. For KNN, is scaling always necessary? | **YES** when features have different units/magnitudes. If features are already on same scale (e.g., all percentages), scaling may not be needed. But as a rule of thumb, always scale for distance-based algorithms. |
| 6. What happens if you scale *after* splitting vs *before*? | **After splitting (correct)**: fit scaler on train only, transform both train and test. **Before splitting (wrong)**: test set information leaks into training — performance estimates become unrealistically optimistic. |

</details>

---

## Exercise J: "Complexity & Curse" — When KNN Fails

| Question | Your Answer |
|----------|-------------|
| 1. What is the time complexity of predicting **one** query with naive KNN? (n = #samples, d = #features) | |
| 2. If you have 1,000,000 samples and 100 features, roughly how many operations per query? | |
| 3. What happens to distances in high-dimensional space? (Curse of Dimensionality) | |
| 4. At what dimensionality do KD-Trees typically become ineffective? | |
| 5. Why would you choose ANN (Approximate NN) over exact KNN? What's the tradeoff? | |
| 6. What is the memory complexity of KNN? | |
| 7. Name one ANN method and briefly explain how it works. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Time complexity of naive KNN per query | **O(n · d)** — need to compute distance to every training point, across d features. |
| 2. Operations for 1M samples, 100 features | **100 million operations** (1,000,000 × 100). Too slow for production. |
| 3. What happens to distances in high-dimensional space? | **Distances equalize**. The ratio of max distance to min distance approaches 1. "Nearest" and "farthest" become indistinguishable. Volume explodes exponentially (2^d corners in a hypercube). Data becomes sparse — every point is an outlier. |
| 4. At what dimensionality do KD-Trees become ineffective? | **d < 20**. Beyond 20 dimensions, pruning becomes ineffective — curse of dimensionality wins. |
| 5. ANN vs exact KNN: tradeoff? | **ANN**: sub-linear query time (O(log n)), scales to billions of points, but sacrifices **perfect accuracy** (returns "probably correct" answers). **Exact KNN**: guaranteed correct answer, but O(n·d) doesn't scale. |
| 6. Memory complexity of KNN | **O(n · d)** — must store the entire training dataset. For 1M samples × 100 features, that's 100M values in memory. |
| 7. Name one ANN method and explain | **HNSW (Hierarchical Navigable Small World)**: Builds a multi-layer graph. Top layers have few nodes with long-range links (coarse navigation). Bottom layers have all nodes with short-range links (fine search). Query starts at top and greedily descends toward query point. O(log n) query time. Powers modern vector databases (Pinecone, Weaviate, FAISS). |

</details>

---

## Exercise K: "Choose the Right Distance"

| Scenario | Best Distance Metric | Why? |
|----------|---------------------|------|
| 1. Text documents represented as word count vectors (TF-IDF) | | |
| 2. House price prediction with features: sqft, bedrooms, bathrooms, year built | | |
| 3. User embeddings from a neural network (d=512) | | |
| 4. Grid-based movement (robot navigating a warehouse) | | |
| 5. Images represented as pixel values (RGB vectors) | | |
| 6. Customer purchase history (binary: bought or not) | | |
| 7. Gene expression data with many zeros | | |

<details>
<summary>📖 Click for Answers</summary>

| Scenario | Best Distance Metric | Why? |
|----------|---------------------|------|
| 1. Text documents (TF-IDF vectors) | **Cosine Similarity** | Focuses on angle (direction) not magnitude. Document length shouldn't affect similarity. |
| 2. House price prediction | **Euclidean (L2)** | Default choice for continuous features after scaling. Intuitive straight-line distance. |
| 3. User embeddings (d=512) | **Euclidean (L2)** or **Cosine** | After training embeddings, both work well. Cosine is common for normalized embeddings. |
| 4. Grid-based movement (robot) | **Manhattan (L1)** | Robot moves in grid patterns (up/down/left/right). Euclidean would cut through walls. |
| 5. Images (RGB pixel vectors) | **Euclidean (L2)** | Standard for pixel-wise comparison. Color intensity differences are meaningful. |
| 6. Customer purchase history (binary) | **Jaccard** or **Cosine** | Binary vectors. Jaccard measures overlap; Cosine works on sets of purchased items. |
| 7. Gene expression with many zeros | **Manhattan (L1)** or **Cosine** | L1 is robust to zeros. Cosine can handle sparse vectors. |

</details>

---

## Exercise L: "Advanced Validation" — LOOCV & Nested CV

| Question | Your Answer |
|----------|-------------|
| 1. What is Leave-One-Out Cross-Validation (LOOCV)? When would you use it? | |
| 2. What is the computational cost of LOOCV compared to 10-fold CV? | |
| 3. What is Nested Cross-Validation? Why would you need it? | |
| 4. You have 150 samples and want to tune hyperparameters AND get an unbiased performance estimate. What validation strategy do you recommend? | |
| 5. For a dataset with 1,000,000 samples, would you use LOOCV? Why/why not? | |
| 6. Compare Holdout, 5-Fold CV, 10-Fold CV, and LOOCV in terms of bias, variance, and compute cost. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What is LOOCV? When to use? | **LOOCV = K=N** (leave one out). Train on N-1 samples, validate on the 1 held-out sample. Repeat N times. **Use when**: dataset is tiny (<100 samples) — maximizes training data per fold. |
| 2. Computational cost of LOOCV vs 10-fold | LOOCV requires **N training runs** (e.g., 1,000 runs). 10-fold requires **10 training runs**. LOOCV is ~100× more expensive for 1,000 samples. |
| 3. What is Nested CV? Why need it? | **Outer loop**: evaluates model performance. **Inner loop**: tunes hyperparameters. Needed when both selecting hyperparameters AND estimating generalization error with an unbiased estimate. Prevents double-dipping (using same data for tuning and evaluation). |
| 4. Strategy for 150 samples | **Nested CV with 5-fold outer, 3-fold inner**. Outer: 5 folds (120 train, 30 validation). Inner (on each outer fold): 3-fold CV to tune hyperparameters. Provides unbiased estimate with 150 samples. |
| 5. Would you use LOOCV for 1M samples? | **NO** — too computationally expensive (1M training runs). Use 5-fold or 10-fold CV instead. |
| 6. Comparison | |

| Method | Compute Cost | Estimate Bias | Estimate Variance | Best For |
|--------|--------------|---------------|-------------------|----------|
| Holdout | Low | Higher | Higher | Large datasets, fast iteration |
| 5-Fold CV | Medium | Moderate | Moderate | General purpose default |
| 10-Fold CV | Medium-High | Lower | Moderate | When accuracy matters |
| LOOCV | Very High | Lowest | Highest | Tiny datasets |

</details>

---

## Exercise M: "Bias-Variance Formula"

| Question | Your Answer |
|----------|-------------|
| 1. Write the Bias-Variance Decomposition formula. | |
| 2. What does each term mean in plain English? | |
| 3. What is the "Irreducible Error" (σ²)? Can we ever eliminate it? | |
| 4. A model has: Bias² = 0.01, Variance = 0.04, σ² = 0.05. What is the total expected error? | |
| 5. How does increasing model complexity affect Bias and Variance? | |
| 6. A model has total error 0.20. If we double the training data, which term decreases? | |
| 7. What does the dartboard analogy represent for each quadrant? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Bias-Variance Decomposition formula | **E[(y - ŷ)²] = Bias²(ŷ) + Var(ŷ) + σ²** |
| 2. What does each term mean? | **Bias²**: How far off the average prediction is from the true value (systematic error). **Var**: How much predictions change across different training sets (instability). **σ²**: Noise inherent in the data (irreducible). |
| 3. What is Irreducible Error? | **σ²** is the noise in the data itself — measurement errors, unmeasured factors. **No model can eliminate it**. It's the floor of achievable error. |
| 4. Total expected error for given values | Total Error = 0.01 + 0.04 + 0.05 = **0.10** |
| 5. How does increasing model complexity affect Bias and Variance? | **Bias decreases** (model becomes more flexible, captures patterns). **Variance increases** (model becomes more sensitive to training data). Tradeoff. |
| 6. Doubling training data — which term decreases? | **Variance** decreases (model becomes more stable). Bias and σ² remain unchanged. |
| 7. Dartboard analogy quadrants | **Low Bias/Low Variance**: Accurate & consistent (bullseye). **Low Bias/High Variance**: Centered but scattered. **High Bias/Low Variance**: Consistently wrong (tight cluster away from bullseye). **High Bias/High Variance**: Wrong & scattered. |

</details>

---

# SECTION 6: COMPLETE COVERAGE

---

## Exercise N: "ML Boom & Expert Systems"

| Question | Your Answer |
|----------|-------------|
| 1. Name the **4 drivers** of the ML boom mentioned in your slides. | |
| 2. What is an Expert System? Give an example. | |
| 3. What was MYCIN? What was its limitation? | |
| 4. What was Deep Blue? How did it differ from modern ML? | |
| 5. What was ELIZA? Why wasn't it "true" AI? | |
| 6. What's the key lesson from expert systems? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. 4 drivers of the ML boom | **1. Data Explosion** (Internet, hospitals, government data). **2. Open-Source Tools** (CUDA, scikit-learn, PyTorch). **3. Cheap Compute** (GPUs, TPUs). **4. Algorithm Advances** (more parallelizable, better training techniques). |
| 2. What is an Expert System? Example | Hand-crafted system where domain experts encode rules. **Example**: Medical diagnosis systems with 600+ rules for bacterial infections. |
| 3. What was MYCIN? Its limitation? | **MYCIN (1970s)**: Medical diagnosis system with 600+ hand-coded rules about bacterial infections. **Limitation**: Doctors had to update every rule manually — doesn't scale. |
| 4. What was Deep Blue? How differ from modern ML? | **Deep Blue (1997)**: Chess engine that beat Kasparov. Evaluated ~200M positions/sec using **handcrafted evaluation functions**, not learned from data. Couldn't generalize to other games (e.g., Go). |
| 5. What was ELIZA? Why not "true" AI? | **ELIZA (1966)**: Chatbot with scripted pattern-matched responses. **Not true AI** because it had zero understanding — just mirrored user input with simple rules. |
| 6. Key lesson from expert systems | **Encoding all human knowledge in rules doesn't scale**. ML learns patterns from data instead. |

</details>

---

## Exercise O: "Beyond the Big Three"

| Question | Your Answer |
|----------|-------------|
| 1. What is **Semi-Supervised Learning**? When would you use it? | |
| 2. What is **Self-Supervised Learning**? Give an example from your slides. | |
| 3. What is **Transfer Learning**? Give an example from your slides. | |
| 4. Why is Semi-Supervised Learning common in practice? | |
| 5. How does Self-Supervised Learning create "labels" without human annotation? | |
| 6. When would you use Transfer Learning instead of training from scratch? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What is Semi-Supervised Learning? When to use? | Uses **small amount of labeled data + large amount of unlabeled data**. Common in practice because **labeling is expensive**. Example: Medical imaging — label 1,000 scans, use 100,000 unlabeled to improve. |
| 2. What is Self-Supervised Learning? Example | Creates **supervision signals from the data itself** — no human labels needed. **Example**: GPT predicts the next word; BERT predicts masked words. Learns rich representations without manual annotation. |
| 3. What is Transfer Learning? Example | Take a model **pre-trained on a large dataset** and **fine-tune it** for your specific task. **Examples**: Fine-tune GPT-4 for customer support; fine-tune ResNet for medical X-rays. |
| 4. Why is Semi-Supervised common in practice? | Labeling is **expensive and time-consuming**. Unlabeled data is abundant. Semi-supervised leverages both to improve performance. |
| 5. How does Self-Supervised create "labels"? | The data itself provides the supervision. For text: predict masked words (BERT) or next word (GPT). For images: predict rotation, colorization, or contrastive tasks. |
| 6. When to use Transfer Learning? | When you have **limited data** for your specific task. Pre-trained models have already learned general features (e.g., edges in images, grammar in language) from massive datasets. Fine-tuning requires far less data. |

</details>

---

## Exercise P: "Applications & Use Cases"

For each application area, list **2 specific use cases** from your slides:

| Application Area | Use Case 1 | Use Case 2 |
|------------------|------------|------------|
| Healthcare | | |
| Transportation | | |
| Finance | | |
| NLP / Language | | |
| Computer Vision | | |
| E-Commerce | | |

**Additional Questions:**

| Question | Your Answer |
|----------|-------------|
| 1. What is the "Cold Start Problem" in recommendation systems? | |
| 2. What are the two main types of recommendation filtering mentioned? | |
| 3. What % of Netflix views come from recommendations? (from your slides) | |
| 4. What % of Amazon sales come from recommendations? (from your slides) | |
| 5. What makes fraud detection difficult for traditional rules? | |

<details>
<summary>📖 Click for Answers</summary>

| Application Area | Use Case 1 | Use Case 2 |
|------------------|------------|------------|
| Healthcare | Cancer detection | Drug discovery |
| Transportation | Self-driving cars | ETA prediction |
| Finance | Fraud detection | Credit scoring |
| NLP / Language | Chatbots/translation | Sentiment analysis |
| Computer Vision | Face unlock | Quality control |
| E-Commerce | Recommendations | Dynamic pricing |

**Additional Questions:**

| Question | Answer |
|----------|--------|
| 1. Cold Start Problem | **New users have no history** → nothing to recommend. Solutions: ask preferences upfront, recommend popular items, or fall back to content-based features. |
| 2. Two types of recommendation filtering | **Collaborative Filtering** ("Users like you also liked...") and **Content-Based Filtering** ("More of what you like..."). |
| 3. % of Netflix views from recs | **75%** of Netflix views come from recommendations. |
| 4. % of Amazon sales from recs | **35%** of Amazon sales come from recommendations. |
| 5. Why fraud detection is difficult for rules | Fraud patterns **evolve constantly** — rules become stale within weeks. Millions of transactions/second can't be manually reviewed. Signals are subtle (time of day, location delta, merchant category). |

</details>

---

## Exercise Q: "The Complete Cheat Sheet"

### Part 1: Fill in all blanks

**Definition of ML (Arthur Samuel, 1959):**
"A field of study that gives computers the ability to learn without being ___________."

**ML Pipeline:**
Data + Algorithm + ________ → Model → ________

**Three Paradigms:**

| Paradigm | Data Type | Goal | Example |
|----------|-----------|------|---------|
| ___________ | Labeled | Map inputs to outputs | Spam detection |
| ___________ | Unlabeled | Find hidden structure | Customer segmentation |
| ___________ | Rewards | Learn by trial and error | Game playing |

**Three-Way Split:**

| Split | Purpose |
|-------|---------|
| ___________ | Fit model parameters |
| ___________ | Tune hyperparameters |
| ___________ | Final unbiased estimate |

**Bias-Variance:**
- High Bias = ___________ (underfitting/overfitting)
- High Variance = ___________ (underfitting/overfitting)
- Total Error = ___________ + ___________ + ___________

**Key Metrics:**

| Metric | Formula | When to Use |
|--------|---------|-------------|
| Accuracy | | |
| Precision | | |
| Recall | | |
| F1 | | |

**Data Leakage:** When information from ___________ leaks into ___________

**Overfitting Fixes:** More data, simpler model, ___________, feature selection

**Underfitting Fixes:** More complex model, more features, ___________ regularization

<details>
<summary>📖 Click for Answers</summary>

**Definition of ML (Arthur Samuel, 1959):**
"A field of study that gives computers the ability to learn without being **explicitly programmed**."

**ML Pipeline:**
Data + Algorithm + **Compute** → Model → **Predictions**

**Three Paradigms:**

| Paradigm | Data Type | Goal | Example |
|----------|-----------|------|---------|
| **Supervised Learning** | Labeled | Map inputs to outputs | Spam detection |
| **Unsupervised Learning** | Unlabeled | Find hidden structure | Customer segmentation |
| **Reinforcement Learning** | Rewards | Learn by trial and error | Game playing |

**Three-Way Split:**

| Split | Purpose |
|-------|---------|
| **Training Set** | Fit model parameters |
| **Validation Set** | Tune hyperparameters |
| **Test Set** | Final unbiased estimate |

**Bias-Variance:**
- High Bias = **Underfitting**
- High Variance = **Overfitting**
- Total Error = **Bias² + Variance + Irreducible Error**

**Key Metrics:**

| Metric | Formula | When to Use |
|--------|---------|-------------|
| Accuracy | (TP + TN) / (TP + TN + FP + FN) | Balanced classes |
| Precision | TP / (TP + FP) | When False Positives are costly |
| Recall | TP / (TP + FN) | When False Negatives are costly |
| F1 | 2 × (P × R) / (P + R) | Imbalanced classes, balance needed |

**Data Leakage:** When information from **the test set** leaks into **training**

**Overfitting Fixes:** More data, simpler model, **regularization**, feature selection

**Underfitting Fixes:** More complex model, more features, **reduce** regularization

</details>

---

# 📊 COMPLETE COVERAGE SUMMARY

| Category | Concepts | Status |
|----------|----------|--------|
| Intro to ML (Lecture 1) | 32 | ✅ 100% |
| Supervised Learning (Lecture 2) | 27 | ✅ 100% |
| Validation & Evaluation (Lecture 3) | 35 | ✅ 100% |
| **TOTAL** | **94** | ✅ **100%** |

---

## 📝 How to Use This Document

1. **Read the question**, write your answer in the blank/box
2. **Click the dropdown** to reveal the model answer
3. **Compare** your answer to the model
4. **Re-study** any sections where you got something wrong
5. **Mark** your confidence level for each topic

---

**Good luck with your exam! 🎯**