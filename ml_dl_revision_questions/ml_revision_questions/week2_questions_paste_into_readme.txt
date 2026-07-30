# 📚 WEEK 2 — COMPLETE STUDY GUIDE
## All Exercises with Answers in Spoiler Format

---

# SECTION 1: LINEAR REGRESSION (Week 2.1)

---

## Exercise LR-1: Linear Model Fundamentals

Answer the following questions about the linear regression model:

| Question | Your Answer |
|----------|-------------|
| 1. Write the linear model equation for a single prediction. Define all terms. | |
| 2. What is the matrix (batch) form of the linear model? | |
| 3. What are the key assumptions of the linear model? | |
| 4. What is the cost function for linear regression? Write it in both forms. | |
| 5. Why is MSE a good choice for the cost function? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Linear model equation | **ŷ = wᵀx + b** where: x ∈ ℝᵈ (input features), w ∈ ℝᵈ (weights/slopes), b ∈ ℝ (bias/intercept), ŷ ∈ ℝ (prediction) |
| 2. Matrix form | **ŷ = Xw** where X ∈ ℝⁿˣ⁽ᵈ⁺¹⁾ (design matrix with bias column appended), w ∈ ℝᵈ⁺¹ |
| 3. Key assumptions | **Linearity**: E[y\|x] = wᵀx + b; **Targets are real-valued** (regression problem); **Features are fixed/non-random** |
| 4. Cost function | **L(w) = (1/n)‖y − Xw‖² = (1/n) Σᵢ (yᵢ − ŷᵢ)²** |
| 5. Why MSE is good | Penalizes large errors more heavily; Differentiable everywhere (easy to optimize); Convex → unique global minimum; Consistent with Gaussian noise (probabilistic view) |

</details>

---

## Exercise LR-2: Normal Equations

| Question | Your Answer |
|----------|-------------|
| 1. Derive the gradient of the MSE cost function. | |
| 2. Set the gradient to zero and derive the normal equations. | |
| 3. What is the closed-form solution for w*? | |
| 4. When does the closed-form solution fail? | |
| 5. What is the computational cost of the normal equations? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Gradient of MSE | **∇w L = −(2/n) Xᵀ(y − Xw)** |
| 2. Normal equations | **Xᵀ(y − Xw) = 0 → XᵀXw = Xᵀy** |
| 3. Closed-form solution | **w* = (XᵀX)⁻¹ Xᵀy** |
| 4. When it fails | When **XᵀX is not invertible** (not full column rank). This happens with multicollinearity or when d > n. |
| 5. Computational cost | **O(nd² + d³)**. For d > 10⁴, prefer iterative gradient descent. |

</details>

---

## Exercise LR-3: Geometric Interpretation

| Question | Your Answer |
|----------|-------------|
| 1. What does ŷ = Xw* represent geometrically? | |
| 2. What is the residual vector e = y − ŷ? What property does it satisfy? | |
| 3. What do the normal equations represent geometrically? | |
| 4. What does OLS find geometrically? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What is ŷ = Xw*? | The **projection of y onto the column space of X (Col(X))**. It's the closest achievable point in the column space. |
| 2. Residual vector | **e = y − ŷ**. It is **perpendicular to every column of X** (orthogonality condition). |
| 3. Normal equations geometrically | **Xᵀe = 0** is exactly the orthogonality condition — residuals are perpendicular to all features. |
| 4. What OLS finds | The **unique point in Col(X) closest to y in Euclidean distance**. |

</details>

---

## Exercise LR-4: Probabilistic Interpretation & MLE

| Question | Your Answer |
|----------|-------------|
| 1. Write the Gaussian noise model for linear regression. | |
| 2. Write the likelihood for a single observation and for all observations. | |
| 3. Derive the log-likelihood and show that MLE = least squares. | |
| 4. What are the noise assumptions? | |
| 5. Derive the MLE for σ² given w*. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Gaussian noise model | **y = wᵀx + b + ε, ε ~ N(0, σ²)**. Conditional distribution: y\|x,w ~ N(wᵀx + b, σ²) |
| 2. Likelihood | Single: **p(yᵢ\|xᵢ,w) = (1/√(2πσ²)) exp(−(yᵢ−wᵀxᵢ)²/2σ²)**. All: **L(w,σ²) = (2πσ²)^(−n/2) exp(−‖y−Xw‖²/2σ²)** |
| 3. MLE = Least Squares | Log-likelihood: **ℓ(w,σ²) = −(n/2)log(2πσ²) − ‖y−Xw‖²/2σ²**. Maximizing ℓ ↔ minimizing ‖y−Xw‖². So **MLE = Ordinary Least Squares**. |
| 4. Noise assumptions | **Zero mean**: E[ε] = 0; **Constant variance**: Var(ε) = σ² (homoscedasticity); **Independence**: εᵢ ⟂ εⱼ for i≠j; **Gaussian**: ε ~ N(0, σ²) |
| 5. MLE for σ² | **σ²* = (1/n)‖y − Xw*‖²** = Mean Squared Error (without the 1/n factor, it's SSE/n) |

</details>

---

## Exercise LR-5: Gauss-Markov Theorem

| Question | Your Answer |
|----------|-------------|
| 1. What does the Gauss-Markov theorem state? | |
| 2. What does "BLUE" stand for and what does it mean? | |
| 3. What are the 5 classical assumptions? | |
| 4. What happens when assumptions fail? | |
| 5. What is the key caveat of Gauss-Markov? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Gauss-Markov theorem | Under the classical OLS assumptions, **w* is the Best Linear Unbiased Estimator (BLUE)**. |
| 2. BLUE meaning | **Best** = Minimum variance among all linear unbiased estimators; **Linear** = Linear function of the output vector y; **Unbiased** = E[w*] equals the true parameter vector. |
| 3. 5 classical assumptions | **A1**: Linearity — E[y\|X] = Xw; **A2**: Random sample — observations i.i.d.; **A3**: No multicollinearity — rank(X) = d+1; **A4**: Zero conditional mean — E[ε\|X] = 0; **A5**: Homoscedasticity — Var(εᵢ\|X) = σ² |
| 4. When assumptions fail | **A3 violated** → XᵀX singular; use Ridge regression. **A4 violated** → biased estimates. **A5 violated** → use WLS or robust standard errors. |
| 5. Key caveat | Gauss-Markov guarantees **linear** unbiased estimators. Non-linear estimators can sometimes have lower variance (e.g., biased estimators like Ridge can have lower MSE). |

</details>

---

## Exercise LR-6: Polynomial Regression

| Question | Your Answer |
|----------|-------------|
| 1. How does polynomial regression extend linear regression? | |
| 2. Write the polynomial feature expansion for degree d. | |
| 3. What stays the same and what changes when using polynomial features? | |
| 4. What controls model complexity in polynomial regression? | |
| 5. What is the key insight about polynomial regression? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Extension | Map input x → feature vector φ(x) = [1, x, x², x³, ..., xᵈ]ᵀ. Then **ŷ = wᵀφ(x)**. |
| 2. Feature expansion | **φ(x) = [1, x, x², x³, ..., xᵈ]ᵀ** |
| 3. What stays same vs changes | **Stays same**: Linear in weights w, normal equations apply, MLE=LS, convex optimization. **Changes**: Non-linear in input x, degree d controls complexity, Φ ∈ ℝⁿˣ⁽ᵈ⁺¹⁾ replaces X ∈ ℝⁿˣ², risk of overfitting grows with d. |
| 4. Complexity control | The **degree d** controls model complexity. Higher d = more flexible = more overfitting risk. |
| 5. Key insight | Non-linear decision boundaries in x-space, but **convex optimization in w-space** — best of both worlds! |

</details>

---

## Exercise LR-7: Bias-Variance Tradeoff

| Question | Your Answer |
|----------|-------------|
| 1. Write the bias-variance decomposition of MSE. | |
| 2. What does each term mean? | |
| 3. What is the "noise floor"? | |
| 4. How does increasing model complexity affect bias and variance? | |
| 5. What do training and validation error curves look like for underfitting, good fit, and overfitting? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Bias-variance decomposition | **MSE = Bias² + Variance + σ²** (where σ² is irreducible noise) |
| 2. Meaning of each term | **Bias²**: How far off the average prediction is from the true value (systematic error). **Variance**: How much predictions change across different training sets (instability). **σ²**: Noise inherent in the data (measurement errors, unmeasured factors). |
| 3. Noise floor | **σ²** cannot be reduced by any model — it sets the best achievable error. |
| 4. Complexity effects | As d increases: **Bias decreases** (more flexible, captures patterns), **Variance increases** (more sensitive to training data). Tradeoff. |
| 5. Error curves | **Underfitting (d=1)**: Both train and val errors high, close together. **Good fit (d=4)**: Train error moderate, val error lowest. **Overfitting (d=9)**: Train error very low, val error very high (large gap). |

</details>

---

## Exercise LR-8: Model Selection via Cross-Validation

| Question | Your Answer |
|----------|-------------|
| 1. Describe the CV process for selecting polynomial degree. | |
| 2. What is the final step after selecting d*? | |
| 3. What is the "test set rule"? | |
| 4. Why must we never inspect test performance during model selection? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. CV process for degree selection | **Step 1**: Candidate set d ∈ {1, 2, ..., D}. **Step 2**: K-fold CV for each d — compute average validation MSE. **Step 3**: Select d* = argmin CV(d). |
| 2. Final step | **Refit** on the full training set with d*. **Report test MSE exactly once**. |
| 3. Test set rule | **Never inspect test performance during model selection**. Doing so leaks information and gives optimistic estimates. |
| 4. Why? | The test set must remain completely untouched until final evaluation. If you tune based on test performance, your test score becomes optimistically biased — it no longer represents how the model will perform on truly unseen data. |

</details>

---

# SECTION 2: REGULARIZATION & TUNING (Week 2.2)

---

## Exercise R-1: Regularization Fundamentals

| Question | Your Answer |
|----------|-------------|
| 1. What is the general form of the regularized objective? | |
| 2. Why do large coefficients cause problems? | |
| 3. Does regularization "make the model worse"? Explain. | |
| 4. Why must features be scaled before regularization? | |
| 5. What is the correct way to scale features in a pipeline? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Regularized objective | **argmin_w [Loss(w) + λ·Penalty(w)]** or equivalently **Loss(w) + λ·Penalty(w)**. Loss measures how wrong predictions are; Penalty enforces preference for certain coefficient patterns (small weights, sparse weights). |
| 2. Why large coefficients are risky | Large weights make predictions very sensitive to small input changes. With correlated features, many weight vectors can fit training data similarly well — regularization chooses simpler/more stable coefficients. |
| 3. Does regularization make the model worse? | **No.** It trades a little training fit for better out-of-sample behavior. It's about improving generalization, not "making it worse." |
| 4. Why scale before regularization? | L1/L2 penalties act on coefficients, not feature effects directly. If features are on different scales, the same coefficient magnitude means very different prediction changes. **Scale matters!** |
| 5. Correct way to scale | Use **Pipeline([("scale", StandardScaler()), ("model", Ridge())])**. Fit scaler on training data only; **never fit scaler on full dataset before splitting** — that leaks test information. |

</details>

---

## Exercise R-2: Ridge Regression (L2)

| Question | Your Answer |
|----------|-------------|
| 1. Write the Ridge regression objective. | |
| 2. What is the effect of L2 regularization on coefficients? | |
| 3. When is Ridge most useful? | |
| 4. In scikit-learn, what does `alpha` represent? | |
| 5. Why does Ridge stabilize correlated features? | |
| 6. How should alpha be searched? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Ridge objective | **argmin_w [Loss(w) + λ·‖w‖₂²]** or **argmin_w [Loss(w) + alpha·‖w‖₂²]** in scikit-learn. |
| 2. Effect on coefficients | Shrinks coefficients **smoothly toward zero**, but usually does **not** set them exactly to zero. |
| 3. When Ridge is useful | Many features; **correlated features**; want stability more than feature selection. |
| 4. `alpha` in scikit-learn | `alpha` is λ (regularization strength). **Larger alpha = stronger regularization = more shrinkage.** |
| 5. Ridge stabilizes correlated features | L2 discourages "large positive + large negative" cancellations. Without Ridge: w₁=9.8, w₂=-8.9 (unstable). With Ridge: w₁=0.7, w₂=0.5 (stable). |
| 6. How to search alpha | Search on a **logarithmic scale**: e.g., 10⁻⁴, 10⁻³, 10⁻², 10⁻¹, 1, 10, 10², 10³, 10⁴. Use validation performance, not prettiest coefficient path. |

</details>

---

## Exercise R-3: Lasso Regression (L1)

| Question | Your Answer |
|----------|-------------|
| 1. Write the Lasso regression objective. | |
| 2. What is the effect of L1 regularization? | |
| 3. When is Lasso most useful? | |
| 4. What is the key difference between Lasso and Ridge? | |
| 5. What are the caveats of Lasso with correlated features? | |
| 6. What is the interpretation of a zero coefficient? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Lasso objective | **argmin_w [Loss(w) + λ·‖w‖₁]** |
| 2. Effect of L1 | Can set coefficients **exactly to zero**. This yields **sparse models** (feature selection). |
| 3. When Lasso is useful | Many features; expect only a subset to matter; need interpretability or variable selection. |
| 4. Key difference from Ridge | **Lasso** = sparse (feature selection). **Ridge** = dense (smooth shrinkage). |
| 5. Caveats with correlated features | Lasso may **arbitrarily choose one feature and ignore another** (selection instability). The selected set can change across samples. |
| 6. Interpretation of zero coefficient | A zero coefficient is **model-dependent**. It is **not proof** that the feature is irrelevant in the real world. |

</details>

---

## Exercise R-4: ElasticNet

| Question | Your Answer |
|----------|-------------|
| 1. Write the ElasticNet objective. | |
| 2. What are the two hyperparameters in ElasticNet? | |
| 3. What is the effect of `l1_ratio` (ρ)? | |
| 4. When is ElasticNet preferred over pure Lasso? | |
| 5. What are the benefits of ElasticNet? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. ElasticNet objective | **argmin_w [Loss(w) + λ·(ρ·‖w‖₁ + (1−ρ)·‖w‖₂²)]** |
| 2. Two hyperparameters | **α** (λ): overall regularization strength. **l1_ratio** (ρ): mixing ratio between L1 and L2. |
| 3. Effect of `l1_ratio` | **ρ = 1** → Pure Lasso (strong sparsity). **ρ = 0** → Pure Ridge (smooth shrinkage). **0 < ρ < 1** → Sparse + stable (often helpful with correlated features). |
| 4. When preferred over Lasso | When features are **correlated**. Pure Lasso may arbitrarily select one; ElasticNet selects groups more stably. |
| 5. Benefits | Combines **sparsity** (L1) with **stability** (L2). Less arbitrary than pure Lasso with correlated features. |

</details>

---

## Exercise R-5: Choosing the Right Regularizer

| Question | Your Answer |
|----------|-------------|
| 1. Which regularizer would you try for many small expected effects? | |
| 2. Which regularizer for sparse feature set needed? | |
| 3. Which regularizer for correlated features + sparsity desired? | |
| 4. Which regularizer for strong interpretability needed? | |
| 5. What's the safe baseline starting point? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Many small effects expected | **Ridge** — Keeps all features, shrinks smoothly |
| 2. Sparse feature set needed | **Lasso** — Can set coefficients to zero |
| 3. Correlated features + sparsity desired | **ElasticNet** — Less arbitrary than pure Lasso |
| 4. Strong interpretability needed | **Lasso / ElasticNet** — Smaller active set is easier to inspect |
| 5. Safe baseline | **Ridge** — Tune alpha before switching families |

</details>

---

## Exercise R-6: Parameters vs Hyperparameters

| Question | Your Answer |
|----------|-------------|
| 1. What is the difference between parameters and hyperparameters? | |
| 2. Give examples of each. | |
| 3. How are parameters learned? How are hyperparameters chosen? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Difference | **Parameters**: Learned by fitting the model. **Hyperparameters**: Chosen outside ordinary fitting (set before training). |
| 2. Examples | **Parameters**: regression coefficients w, intercept b. **Hyperparameters**: alpha, l1_ratio, polynomial degree, k in KNN. |
| 3. How they're learned/chosen | **Training** learns parameters. **Validation** chooses hyperparameters. |

</details>

---

## Exercise R-7: Grid Search vs Random Search

| Question | Your Answer |
|----------|-------------|
| 1. How does grid search work? | |
| 2. What is the cost of grid search? | |
| 3. How does random search work? | |
| 4. Why is random search often more efficient? | |
| 5. When would you choose grid search over random search? | |
| 6. What sampling distribution would you use for alpha? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Grid search | Define a fixed set of values for each hyperparameter and evaluate **every combination**. |
| 2. Cost of grid search | Cost grows **multiplicatively** with each extra hyperparameter. If 10 values × 10 values = 100 combinations. |
| 3. Random search | Specify distributions or ranges, then sample hyperparameter settings at **random**. |
| 4. Why random search is more efficient | Covers more distinct values of each hyperparameter under the same budget. Only a few hyperparameters usually really matter. |
| 5. When to choose grid | Few hyperparameters and good prior ranges. Simple and reproducible. |
| 6. Sampling distribution for alpha | **log-uniform(10⁻⁴, 10⁴)** — alpha matters over orders of magnitude. |

</details>

---

## Exercise R-8: Cross-Validation Inside Hyperparameter Search

| Question | Your Answer |
|----------|-------------|
| 1. How does cross-validation work inside hyperparameter search? | |
| 2. Why use CV instead of a single validation split? | |
| 3. What is the validation protocol for tuning? | |
| 4. What does `search.best_estimator_` give you? | |
| 5. What are common leakage mistakes during tuning? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. CV inside search | For each candidate hyperparameter setting: fit K models (on K−1 folds, validate on held-out fold), average validation scores. |
| 2. Why use CV instead of single split | Reduces dependence on one lucky or unlucky validation split. More reliable estimate. |
| 3. Validation protocol | **Train**: Fit candidate models. **Validation/CV**: Choose hyperparameters. **Test**: Estimate final performance once. |
| 4. `search.best_estimator_` | The best model (pipeline) refit on all training data with the best hyperparameters. |
| 5. Common leakage mistakes | **Leakage 1**: Scaling/imputing before train/test split. **Leakage 2**: Selecting features using full dataset before CV. **Leakage 3**: Looking at test performance repeatedly while deciding hyperparameters. |

</details>

---

## Exercise R-9: Nested Cross-Validation

| Question | Your Answer |
|----------|-------------|
| 1. What is nested cross-validation? | |
| 2. Why do we need nested CV? | |
| 3. What is the computational cost of nested CV? | |
| 4. When would you use nested CV vs train/validation/test? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Nested CV | **Outer loop**: evaluates model performance. **Inner loop**: tunes hyperparameters within each outer training fold. |
| 2. Why nested CV? | Estimates the performance of the **entire model-selection procedure**. Gives unbiased estimate when both selecting hyperparameters AND evaluating performance. |
| 3. Computational cost | **Candidates × inner folds × outer folds**. Very expensive. |
| 4. When to use | **Nested CV**: Careful benchmarking, small datasets, final reports. **Train/validation/test**: Many practical projects. |

</details>

---

## Exercise R-10: Learning Curves — Diagnosis

| Question | Your Answer |
|----------|-------------|
| 1. What is a learning curve? | |
| 2. What does it mean if training and validation scores are both low and close together? | |
| 3. What does it mean if training score is much higher than validation score (large gap)? | |
| 4. What does it mean if the validation curve is still rising at the largest dataset size? | |
| 5. What does it mean if both curves plateau below the desired target? | |
| 6. What is the difference between a learning curve and a validation curve? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Learning curve | Model performance as a function of **training set size**. |
| 2. Low train + low val, close together | **High Bias / Underfitting**. Try: more flexible model, better features, reduce regularization, train longer. |
| 3. High train + lower val, large gap | **High Variance / Overfitting**. Try: more data, stronger regularization, simpler model, feature selection, ensembling. |
| 4. Validation curve still rising | **Data-limited**. More data is likely to help. |
| 5. Both plateau below target | **Noise-limited** (or missing signal). Labels/features may be noisy. Focus on features, labels, loss function, or problem formulation. |
| 6. Learning curve vs Validation curve | **Learning curve**: x-axis = training set size; answers "would more data help?" **Validation curve**: x-axis = hyperparameter value; answers "what value controls under/overfit?" |

</details>

---

## Exercise R-11: Diagnosis Table

| Question | Your Answer |
|----------|-------------|
| 1. Train low, Valid low, small gap → diagnose and fix | |
| 2. Train high, Valid lower, large gap → diagnose and fix | |
| 3. Valid still rising with data → diagnose and fix | |
| 4. Both plateau below target → diagnose and fix | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Train low, Valid low, small gap | **High Bias**. Fix: increase flexibility; lower regularization. |
| 2. Train high, Valid lower, large gap | **High Variance**. Fix: more data; stronger regularization. |
| 3. Valid still rising with data | **Data-limited**. Fix: collect more data; use augmentation. |
| 4. Both plateau below target | **Noise / Missing signal**. Fix: improve labels, features, objective. |

</details>

---

## Exercise R-12: Common Pitfalls in Tuning

| Question | Your Answer |
|----------|-------------|
| 1. What happens if you tune on the test set? | |
| 2. Why is feature scaling important before regularization? | |
| 3. What happens if you search alpha on a linear grid [1,2,3]? | |
| 4. What does low train and low validation scores mean? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Tuning on test set | **Leakage**. Test set becomes part of training decisions; reported performance becomes optimistically biased. |
| 2. Feature scaling importance | Regularization strength becomes **feature-scale dependent**. Without scaling, coefficients for large-range features are penalized differently. |
| 3. Linear grid for alpha | **Misses that alpha matters over orders of magnitude**. Should use log scale (e.g., 10⁻⁴, 10⁻³, ...). |
| 4. Low train and validation scores | **High bias**. Calls for more flexibility, not stronger regularization! |

</details>

---

# SECTION 3: LOGISTIC REGRESSION & NAIVE BAYES (Week 2.3)

---

## Exercise LRG-1: Logistic Regression Fundamentals

| Question | Your Answer |
|----------|-------------|
| 1. What is the logistic (sigmoid) function? Write its equation. | |
| 2. How does logistic regression convert a linear score to a probability? | |
| 3. What is the decision boundary for logistic regression? | |
| 4. What happens to p(y=1\|x) when z is negative vs positive? | |
| 5. How do you get class predictions from probabilities? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Sigmoid function | **σ(z) = 1 / (1 + e⁻ᶻ)**. Maps any real number to (0,1). |
| 2. Linear score → probability | **z = wᵀx + b**, then **p(y=1\|x) = σ(z) = 1 / (1 + e⁻(wᵀx+b))** |
| 3. Decision boundary | **wᵀx + b = 0** (a hyperplane). At threshold 0.5: σ(z) ≥ 0.5 ⇔ z ≥ 0. |
| 4. Negative vs positive z | **Negative score** → p < 0.5. **Positive score** → p ≥ 0.5. |
| 5. Class predictions | **ŷ = 1** if p(y=1\|x) ≥ threshold (default 0.5), else **ŷ = 0**. |

</details>

---

## Exercise LRG-2: Training Logistic Regression

| Question | Your Answer |
|----------|-------------|
| 1. What is the likelihood for logistic regression? | |
| 2. What is the loss function (binary cross-entropy)? | |
| 3. Why is there no closed-form solution? | |
| 4. What does MLE give us in logistic regression? | |
| 5. How does logistic regression relate to linear regression? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Likelihood | **P(y\|x) = pʸ(1−p)¹⁻ʸ** where p = P(y=1\|x). For all data: product over i. |
| 2. Binary cross-entropy loss | **−[y log p + (1−y) log(1−p)]** |
| 3. No closed-form solution | Unlike linear regression, there is no closed-form normal equation; optimization is **iterative**. |
| 4. What MLE gives us | Choose parameters that make observed labels likely. Confident wrong predictions get a large penalty. |
| 5. Connection to linear regression | Same MLE logic, different observation model. Linear regression: Gaussian noise. Logistic regression: Bernoulli observation model. |

</details>

---

## Exercise LRG-3: Regularized Logistic Regression

| Question | Your Answer |
|----------|-------------|
| 1. How does regularization carry over to classification? | |
| 2. What are L2, L1, and ElasticNet in logistic regression? | |
| 3. What is the effect of L2 regularization in logistic regression? | |
| 4. What is the effect of L1 regularization in logistic regression? | |
| 5. In scikit-learn, what is `C` and how does it relate to regularization? | |
| 6. Why scale continuous features before regularized linear models? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Regularization carries over | **loss(data; w,b) + λ·penalty(w)**. L1/L2 penalties apply to logistic loss instead of squared error. |
| 2. L2, L1, ElasticNet | **L2/Ridge**: shrinks coefficients; stable default. **L1/Lasso**: can drive coefficients to zero; useful for sparse feature selection. **ElasticNet**: mix of both. |
| 3. L2 effect | Shrinks all coefficients smoothly toward zero. |
| 4. L1 effect | Can set coefficients exactly to zero (sparse feature selection). |
| 5. `C` in scikit-learn | **C = 1/λ**. Smaller C means **stronger regularization**. |
| 6. Why scale | Penalties act on coefficients, not feature effects directly. Must scale continuous features before regularized linear models. |

</details>

---

## Exercise LRG-4: Interpreting Coefficients

| Question | Your Answer |
|----------|-------------|
| 1. What is the logit (log-odds)? | |
| 2. How do we interpret a coefficient in logistic regression? | |
| 3. If hours studied coefficient = +0.7, what does that mean? | |
| 4. If missed assignments coefficient = −1.2, what does that mean? | |
| 5. How do we make coefficient magnitudes comparable? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Logit | **logit(p) = log(p/(1−p)) = wᵀx + b** |
| 2. Coefficient interpretation | Increase feature xⱼ by 1 ⇒ **log-odds changes by wⱼ**. Coeffs are linear effects on log-odds, not directly on probability. |
| 3. hours studied = +0.7 | Each additional hour of study increases the log-odds of passing by 0.7 (higher odds of passing). |
| 4. missed assignments = −1.2 | Each additional missed assignment decreases the log-odds of passing by 1.2 (lower odds of passing). |
| 5. Make magnitudes comparable | Use **standardized features**. Coefficient magnitudes become more comparable when features are scaled. |

</details>

---

## Exercise LRG-5: Multiclass Logistic Regression

| Question | Your Answer |
|----------|-------------|
| 1. What are the two common approaches for multiclass classification? | |
| 2. How does One-vs-Rest (OvR) work? | |
| 3. How does Softmax/Multinomial work? | |
| 4. What is the softmax function? | |
| 5. Which is the natural multiclass generalization theoretically? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Two common approaches | **One-vs-Rest (OvR)** and **Softmax/Multinomial**. |
| 2. One-vs-Rest | Train K binary classifiers: "class k" vs "not class k". Predict ŷ = argmaxⱼ scoreⱼ(x). |
| 3. Softmax/Multinomial | Train one model with K scores normalized into probabilities. |
| 4. Softmax function | **p(y=k\|x) = exp(zⱼ) / Σⱼ exp(zⱼ)** |
| 5. Natural multiclass generalization | **Softmax** is the natural multiclass generalization theoretically. |

</details>

---

## Exercise LRG-6: Thresholds & Decision Making

| Question | Your Answer |
|----------|-------------|
| 1. What is the default threshold in scikit-learn? | |
| 2. What happens when you increase the threshold? | |
| 3. What happens when you decrease the threshold? | |
| 4. How should you choose the threshold? | |
| 5. What tradeoff does changing the threshold involve? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Default threshold | **0.5** in scikit-learn. |
| 2. Increase threshold | Fewer positives, usually **higher precision** and **lower recall**. |
| 3. Decrease threshold | More positives, usually **lower precision** and **higher recall**. |
| 4. How to choose threshold | Choose using **validation data** and the **real cost of errors**. |
| 5. Tradeoff | **Precision vs Recall** tradeoff. Higher threshold = fewer false positives (higher precision) but more false negatives (lower recall). |

</details>

---

## Exercise LRG-7: ROC Curve & AUC

| Question | Your Answer |
|----------|-------------|
| 1. What does ROC stand for and what does it plot? | |
| 2. What does the AUC represent? | |
| 3. What is AUC for a random classifier? | |
| 4. What is AUC for a perfect classifier? | |
| 5. Why is AUC threshold-independent? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. ROC | **Receiver Operating Characteristic**. Plots **True Positive Rate** vs **False Positive Rate** across all thresholds. |
| 2. AUC | Area Under the ROC Curve. Higher is better. |
| 3. Random classifier AUC | **0.5** (diagonal line). |
| 4. Perfect classifier AUC | **1.0** (perfect separation). |
| 5. Threshold-independent | Summarizes performance across **all thresholds**, not just one. |

</details>

---

## Exercise LRG-8: Discriminative vs Generative

| Question | Your Answer |
|----------|-------------|
| 1. What does a discriminative model model? | |
| 2. What does a generative model model? | |
| 3. Which type is logistic regression? | |
| 4. Which type is Naive Bayes? | |
| 5. What is the key difference in their assumptions? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Discriminative model | Models **P(y\|x)** — learns the boundary directly. |
| 2. Generative model | Models **P(x\|y) and P(y)** — models how each class generates data. |
| 3. Logistic regression type | **Discriminative** model. |
| 4. Naive Bayes type | **Generative** model. |
| 5. Key difference | Logistic regression: learns boundary directly. Naive Bayes: models how each class could generate the data. |

</details>

---

## Exercise LRG-9: Bayes' Rule for Classification

| Question | Your Answer |
|----------|-------------|
| 1. Write Bayes' rule for classification. | |
| 2. What does P(y) represent? | |
| 3. What does P(x\|y) represent? | |
| 4. Why can we ignore P(x) for classification? | |
| 5. How do we choose the class in Naive Bayes? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Bayes' rule | **P(y\|x) = P(x\|y)·P(y) / P(x)** |
| 2. P(y) | **Prior probability** of the class (before seeing features). |
| 3. P(x\|y) | **Likelihood** of the observed features under that class. |
| 4. Ignore P(x) | P(x) is the **same for every class**, so it can be ignored for argmax classification. |
| 5. Class choice | **argmaxᵧ P(x\|y)·P(y)** (choose class with highest posterior). |

</details>

---

## Exercise LRG-10: The "Naive" Assumption

| Question | Your Answer |
|----------|-------------|
| 1. What is the "naive" assumption in Naive Bayes? | |
| 2. Write the mathematical expression for the assumption. | |
| 3. Is the assumption true in real data? | |
| 4. Why does Naive Bayes still work well despite the assumption? | |
| 5. What is a classic example where Naive Bayes is a strong baseline? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. "Naive" assumption | Features are **conditionally independent given the class**. |
| 2. Mathematical expression | **P(x₁, x₂, ..., x_d \| y) ≈ Πⱼ P(xⱼ \| y)** |
| 3. Is it true? | **Often false in real data**. Text: words are not independent. |
| 4. Why still works? | Can still work surprisingly well for classification. Decoupling features makes estimation easy. |
| 5. Classic example | **Text classification** — Naive Bayes is a strong baseline despite words not being independent. |

</details>

---

## Exercise LRG-11: Naive Bayes Variants

| Question | Your Answer |
|----------|-------------|
| 1. What are the three common Naive Bayes variants? | |
| 2. When would you use Gaussian NB? | |
| 3. When would you use Bernoulli NB? | |
| 4. When would you use Multinomial NB? | |
| 5. Which is usually the first choice for text classification? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Three variants | **Gaussian NB**, **Bernoulli NB**, **Multinomial NB**. |
| 2. Gaussian NB | For **continuous features** (xⱼ\|y ~ Normal). |
| 3. Bernoulli NB | For **binary indicators** (word present / absent). |
| 4. Multinomial NB | For **counts or frequencies** (word counts in documents). |
| 5. First choice for text | **MultinomialNB** is usually the first Naive Bayes model to try for text classification. |

</details>

---

## Exercise LRG-12: Multinomial Naive Bayes for Text

| Question | Your Answer |
|----------|-------------|
| 1. How is a document represented in Multinomial Naive Bayes? | |
| 2. Write the scoring equation for Multinomial NB. | |
| 3. Why use log probabilities? | |
| 4. How do counts affect the prediction? | |
| 5. How do class priors help? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Document representation | As **word counts** vector. Each document is a vector of counts for each vocabulary word. |
| 2. Scoring equation | **score(y) = log P(y) + Σⱼ countⱼ · log P(wordⱼ \| y)** |
| 3. Why log probabilities | Use **log probabilities** to avoid numerical underflow (multiplying many small probabilities). |
| 4. Counts effect | Counts add evidence: **repeated words matter**. More occurrences of a word = stronger evidence. |
| 5. Class priors | Class priors help when classes are **imbalanced**. |

</details>

---

## Exercise LRG-13: Laplace Smoothing

| Question | Your Answer |
|----------|-------------|
| 1. Why do we need Laplace smoothing? | |
| 2. Write the formula for Laplace smoothing. | |
| 3. What problem does it solve? | |
| 4. What happens to P(word\|class) for an unseen word without smoothing? | |
| 5. What is α in the smoothing formula? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why smoothing | **Unseen words should not make a whole class impossible.** |
| 2. Smoothing formula | **P(word\|class) = (count(word,class) + α) / (total_words_in_class + α·\|V\|)** where \|V\| is vocabulary size. |
| 3. Problem solved | Prevents **zero probabilities** for words not seen in training. |
| 4. Without smoothing | If "quantum" never appears in training spam, P(quantum\|spam)=0. A spam document containing "quantum" gets score 0. |
| 5. What is α | **α** is the smoothing parameter. Adds α pseudo-counts so every vocabulary word has a small nonzero probability. |

</details>

---

## Exercise LRG-14: Logistic Regression vs Naive Bayes

| Question | Logistic Regression | Naive Bayes |
|----------|---------------------|-------------|
| 1. What is modeled? | | |
| 2. Main assumption | | |
| 3. Typical text behavior | | |
| 4. Feature scaling needed? | | |
| 5. Rule of thumb | | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Logistic Regression | Naive Bayes |
|----------|---------------------|-------------|
| 1. What is modeled? | **P(y\|x)** | **P(x\|y) and P(y)** |
| 2. Main assumption | **Linear decision boundary** | **Conditional independence** |
| 3. Typical text behavior | Strong with enough data + regularization | Fast, strong with small data |
| 4. Feature scaling needed? | **Important** for numeric features | Variant dependent |
| 5. Rule of thumb | **Try both as baselines** on text problems; let validation decide. |

</details>

---

## Exercise LRG-15: Text Classification Pipeline

| Question | Your Answer |
|----------|-------------|
| 1. What is the text classification pipeline? | |
| 2. What is Bag-of-Words (BoW)? | |
| 3. What are the pros of BoW? | |
| 4. What are the cons of BoW? | |
| 5. Why must validation include the vectorizer inside the pipeline? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Pipeline | **raw documents → tokenize → vectorize → classifier → label** |
| 2. Bag-of-Words | Ignore word order; count how often each vocabulary term appears. |
| 3. Pros of BoW | Simple, interpretable, fast, often strong. |
| 4. Cons of BoW | Loses word order, phrase structure, and many semantic details. |
| 5. Why include vectorizer in pipeline | Vocabulary and IDF are learned from data. Must be fit on **training data only** to prevent leakage. |

</details>

---

## Exercise LRG-16: TF-IDF

| Question | Your Answer |
|----------|-------------|
| 1. What does TF-IDF stand for? | |
| 2. Write the TF-IDF formula. | |
| 3. What is the effect of TF-IDF? | |
| 4. What does IDF do? | |
| 5. Why does TF-IDF often improve linear text classifiers? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. TF-IDF | **Term Frequency — Inverse Document Frequency**. |
| 2. TF-IDF formula | **tf-idf(term, doc) = tf(term, doc) × idf(term)** where idf(term) ≈ log(N / df(term)). |
| 3. Effect | Count words, but **discount very common words**. |
| 4. What IDF does | High-frequency corpus words like "the" get small weights. Rare but document-relevant terms get larger weights. |
| 5. Why improves classifiers | TF-IDF often **improves linear text classifiers** by weighting words by importance (rare words get more weight). |

</details>

---

## Exercise LRG-17: Leakage Avoidance with Text

| Question | Your Answer |
|----------|-------------|
| 1. What is the bad workflow for text features? | |
| 2. Why does the bad workflow cause leakage? | |
| 3. What is the good workflow? | |
| 4. What is the key principle for text feature engineering? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Bad workflow | Fit vectorizer on **all documents**, then split into train/test. |
| 2. Why bad | **Test-set words and document frequencies** can influence the feature space before evaluation. |
| 3. Good workflow | **Split first**; fit vectorizer inside train-only pipeline. |
| 4. Key principle | All feature engineering must be **fit on training data only**. Never let test data influence preprocessing. |

</details>

---

## Exercise LRG-18: Diagnosing Text Classifiers

| Question | Your Answer |
|----------|-------------|
| 1. Many false positives → suggested actions | |
| 2. Rare class has low recall → suggested actions | |
| 3. Train high, test low → suggested actions | |
| 4. Model ignores phrases → suggested actions | |
| 5. What is the most important source of improvements? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Many false positives | Raise threshold; inspect misleading tokens; add negative examples |
| 2. Rare class low recall | Class weights; more data; threshold adjustment; macro-F1 |
| 3. Train high, test low | Regularize more; reduce vocabulary; check leakage/split |
| 4. Model ignores phrases | Try bigrams; tune ngram_range |
| 5. Most important | Most improvements come from **inspecting errors**, not just trying bigger models. |

</details>

---

# 📊 COMPLETE COVERAGE SUMMARY

| Category | Concepts | Status |
|----------|----------|--------|
| Linear Regression | All major concepts | ✅ 100% |
| Regularization & Tuning | All major concepts | ✅ 100% |
| Logistic Regression & Naive Bayes | All major concepts | ✅ 100% |
| **TOTAL** | **All Week 2 concepts** | ✅ **100%** |

---

## 📝 How to Use This Document

1. **Read the question**, write your answer in the blank/box
2. **Click the dropdown** to reveal the model answer
3. **Compare** your answer to the model
4. **Re-study** any sections where you got something wrong
5. **Mark** your confidence level for each topic

---

**Good luck with your exam! 🎯**