# 📚 WEEK 4 — COMPLETE STUDY GUIDE
## All Exercises with Answers in Spoiler Format

---

# SECTION 1: IMBALANCED DATASETS

---

## Exercise ID-1: The Problem — What is Class Imbalance?

| Question | Your Answer |
|----------|-------------|
| 1. What is class imbalance? | |
| 2. Give 3 real-world examples of imbalanced datasets with typical ratios. | |
| 3. What is the "accuracy paradox"? | |
| 4. Why do naive models fail on imbalanced data mechanically? | |
| 5. What are the three families of solutions for class imbalance? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What is class imbalance? | When one class has far fewer samples than another. It is the norm, not the exception, in real-world data. |
| 2. Real-world examples | **Credit fraud**: 99.7% / 0.3%. **Medical diagnosis**: 95.0% / 5.0%. **Email spam**: 85.0% / 15.0%. **Churn detection**: 80.0% / 20.0%. |
| 3. Accuracy paradox | A classifier that predicts the majority class for every sample achieves high accuracy but is completely useless. E.g., 99.7% accuracy on fraud data while catching 0 fraud cases. |
| 4. Why models fail mechanically | **Loss functions treat all samples equally** → majority samples dominate gradients. **Decision boundary shifts toward majority class** → minimizing errors on majority = lowest total loss. **Model never sees enough minority examples** → can't learn their pattern reliably. |
| 5. Three families of solutions | **1. Data-Level**: Modify training data to balance classes (oversampling, undersampling, SMOTE). **2. Algorithm-Level**: Tell model minority errors cost more (class_weight, focal loss). **3. Metric & Threshold**: Evaluate and deploy at right operating point (precision/recall/F1, threshold tuning). |

</details>

---

## Exercise ID-2: Measuring Imbalance Severity

| Question | Your Answer |
|----------|-------------|
| 1. What is the imbalance ratio for a 1:500 dataset? | |
| 2. What is the severity for 1:2 to 1:5 imbalance? | |
| 3. What is the severity for 1:10 to 1:50 imbalance? | |
| 4. What is the severity for 1:100 to 1:500 imbalance? | |
| 5. What is the severity for 1:500+ imbalance? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Imbalance ratio for 1:500 | **1:500** (one minority sample for every 500 majority samples). Example: 2,000 fraud / 1,000,000 legitimate. |
| 2. 1:2 to 1:5 | **Mild** — e.g., churn (20% churn rate) |
| 3. 1:10 to 1:50 | **Moderate** — e.g., medical diagnosis |
| 4. 1:100 to 1:500 | **Severe** — e.g., credit fraud, rare disease |
| 5. 1:500+ | **Extreme** — e.g., cyber attack, asteroid hits |

</details>

---

## Exercise ID-3: Resampling Strategies — Random Oversampling

| Question | Your Answer |
|----------|-------------|
| 1. How does Random Oversampling work? | |
| 2. What are the pros of Random Oversampling? | |
| 3. What are the cons of Random Oversampling? | |
| 4. What is the risk of oversampling? | |
| 5. With original {Legit: 9970, Fraud: 30}, what does ROS produce? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. How ROS works | Randomly duplicate minority samples until balance is achieved. |
| 2. Pros | Extremely simple, works with any model, no information loss from majority, preserves original feature distributions. |
| 3. Cons | High risk of overfitting on duplicated samples, greatly increases training time (more data), adds no new signal — model memorizes copies. |
| 4. Risk | Model memorizes exact copies → overfitting to minority class. |
| 5. ROS output | After ROS: {Legit: 9970, Fraud: 9970} — no new information, just duplicates. |

</details>

---

## Exercise ID-4: Resampling Strategies — Random Undersampling

| Question | Your Answer |
|----------|-------------|
| 1. How does Random Undersampling work? | |
| 2. What are the pros of Random Undersampling? | |
| 3. What are the cons of Random Undersampling? | |
| 4. With original {Legit: 9970, Fraud: 30}, what does RUS produce? | |
| 5. Is 1:1 always the best balance? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. How RUS works | Randomly remove majority samples until balance is achieved. |
| 2. Pros | Faster training (much less data), no overfitting from duplicates, reduces majority class noise, very fast to compute. |
| 3. Cons | Discards potentially useful majority samples, high variance (which samples removed), severe undersampling can hurt majority recall, information loss. |
| 4. RUS output | After RUS: {Legit: 30, Fraud: 30} — radically reduces training data! |
| 5. Is 1:1 always best? | No — treating balance ratio as hyperparameter often yields better results (e.g., 10:1 or 5:1 can outperform perfect balance). |

</details>

---

## Exercise ID-5: SMOTE — Synthetic Minority Oversampling

| Question | Your Answer |
|----------|-------------|
| 1. What does SMOTE stand for? | |
| 2. How does SMOTE generate synthetic samples? | |
| 3. Write the SMOTE formula. | |
| 4. What are the SMOTE variants and when to use them? | |
| 5. Why is SMOTE better than random oversampling? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. SMOTE stands for | **Synthetic Minority Over-sampling Technique** |
| 2. How SMOTE works | For each minority sample: find K nearest neighbors (K=5), randomly select one neighbor, generate synthetic sample by interpolating between them. |
| 3. SMOTE formula | **x_new = x_i + λ × (x_j − x_i)** where λ ~ Uniform(0, 1) |
| 4. SMOTE variants | **SMOTE**: random interpolation between k neighbors. **SMOTE-NC**: handles categorical features. **BorderlineSMOTE**: synthesis near decision boundary only. |
| 5. Why SMOTE > ROS | Adds **new information** rather than duplicating existing points — interpolates to create realistic new samples. |

</details>

---

## Exercise ID-6: Intelligent Undersampling — Tomek Links & NearMiss

| Question | Your Answer |
|----------|-------------|
| 1. What is a Tomek Link? | |
| 2. What does removing Tomek Links do? | |
| 3. What are the NearMiss variants? | |
| 4. When would you use Tomek Links? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Tomek Link | A pair of samples from opposite classes that are each other's nearest neighbor. |
| 2. Removing Tomek Links | Removes noisy boundary majority samples — cleans decision boundary without large data loss. |
| 3. NearMiss variants | **NearMiss-1**: majority samples with smallest avg distance to 3 nearest minority points. **NearMiss-2**: majority samples with smallest avg distance to 3 farthest minority points. **NearMiss-3**: majority samples farthest from any minority sample. |
| 4. When to use Tomek Links | Use after SMOTE to clean overlapping samples near decision boundary (SMOTE + Tomek = SMOTETomek). |

</details>

---

## Exercise ID-7: Critical — Never Resample the Test Set

| Question | Your Answer |
|----------|-------------|
| 1. What is the wrong (leakage) pattern? | |
| 2. What is the correct pipeline pattern? | |
| 3. Why is resampling the test set a problem? | |
| 4. What tool should you use for safe CV with resampling? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Wrong pattern | `smote.fit_resample(X, y)` on **entire dataset**, then split into train/test. Test gets synthetic samples. |
| 2. Correct pattern | Split first: `X_train, X_test, y_train, y_test = train_test_split(X, y, stratify=y)`. Then resample ONLY training data: `smote.fit_resample(X_train, y_train)`. |
| 3. Why it's a problem | Synthetic test samples don't represent real-world distribution → inflated metrics. |
| 4. Safe tool | Use `imblearn.pipeline.Pipeline` — applies resampling only inside CV folds automatically. `sklearn.pipeline.Pipeline` does NOT work for resampling! |

</details>

---

## Exercise ID-8: Class Weights

| Question | Your Answer |
|----------|-------------|
| 1. How do class weights work? | |
| 2. What does `class_weight='balanced'` compute? | |
| 3. For 9970 legit and 30 fraud, what are the balanced weights? | |
| 4. What are the pros of class weights vs resampling? | |
| 5. What are the cons of class weights? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. How class weights work | Instead of changing the data, change what it costs the model to make errors. Misclassifying a minority sample is penalized more heavily. |
| 2. `class_weight='balanced'` formula | **w_c = n_samples / (n_classes × n_c)** |
| 3. Balanced weights for 9970/30 | w_legit = 10000 / (2 × 9970) ≈ 0.50; w_fraud = 10000 / (2 × 30) ≈ 166.7. Fraud errors penalized **333× more**! |
| 4. Pros | No data modification, fast training, supported by almost all sklearn models, works inside CV safely, no overfitting risk from duplicates, interpretable explicit cost ratios. |
| 5. Cons | Doesn't add new minority information, very severe imbalance may still need resampling, some models respond differently, custom ratios require domain expertise. |

</details>

---

## Exercise ID-9: Focal Loss

| Question | Your Answer |
|----------|-------------|
| 1. What is Focal Loss and who introduced it? | |
| 2. How does Focal Loss work? | |
| 3. What does γ control? | |
| 4. When should you use Focal Loss? | |
| 5. What is the key advantage of Focal Loss for imbalanced data? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Focal Loss | Introduced by **Facebook AI for object detection**. Dynamically re-weights loss so hard-to-classify examples (often minority class) dominate training. |
| 2. How it works | Down-weights easy examples (γ=2 standard setting). Focuses training on hard-to-classify examples. |
| 3. What γ controls | **γ = 0** → standard cross-entropy. **γ = 2** → standard focal setting (focus on hard). |
| 4. When to use | Deep learning classifiers on highly imbalanced data, object detection (many background patches), NLP sentiment on rare categories. |
| 5. Key advantage | Dynamically focuses on minority examples during training — they become the "hard" examples the model pays attention to. |

</details>

---

## Exercise ID-10: Evaluation Metrics — Precision, Recall, F1

| Question | Your Answer |
|----------|-------------|
| 1. What does Precision measure? | |
| 2. What does Recall measure? | |
| 3. What does F1 measure? | |
| 4. When should you optimize Precision? | |
| 5. When should you optimize Recall? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Precision | **TP / (TP + FP)** — "Of all instances I flagged as positive, what % were actually positive?" Quality of positives. |
| 2. Recall | **TP / (TP + FN)** — "Of all actual positives, what % did I catch?" Coverage of actual positives. |
| 3. F1 | **2 × (P × R) / (P + R)** — Harmonic mean of Precision and Recall. Punishes extreme imbalance between P and R. |
| 4. When to optimize Precision | When **FP is costly** — spam filter blocks valid emails, expensive biopsy unnecessary. |
| 5. When to optimize Recall | When **FN is costly** — cancer screening, fraud detection, disaster warning. |

</details>

---

## Exercise ID-11: ROC-AUC vs PR-AUC

| Question | Your Answer |
|----------|-------------|
| 1. What does ROC-AUC plot? | |
| 2. What does PR-AUC plot? | |
| 3. Why is ROC-AUC misleading for imbalanced data? | |
| 4. Why is PR-AUC better for imbalanced data? | |
| 5. For fraud data with 0.1% fraud, random classifier ROC-AUC and PR-AUC? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. ROC-AUC | Plots **TPR (Recall) vs FPR** at every threshold. Random = 0.5, Perfect = 1.0. |
| 2. PR-AUC | Plots **Precision vs Recall** at every threshold. Random ≈ minority class prevalence, Perfect = 1.0. |
| 3. Why ROC-AUC is misleading | With 9,970 negatives, FPR = FP/(FP+TN) stays near 0 even with many FPs. ROC curve looks great even for a bad model. |
| 4. Why PR-AUC is better | FP dominates precision denominator — no hiding. Reveals minority class performance honestly. **PR-AUC is preferred for imbalanced problems.** |
| 5. Random classifier for 0.1% fraud | **ROC-AUC = 0.5** (always). **PR-AUC ≈ 0.001** (minority class prevalence). PR-AUC = 0.43 is much better than chance! |

</details>

---

## Exercise ID-12: Moving the Decision Threshold

| Question | Your Answer |
|----------|-------------|
| 1. Why is the default threshold of 0.5 problematic for imbalanced problems? | |
| 2. How do you find the optimal threshold? | |
| 3. What happens when you lower the threshold? | |
| 4. What happens when you raise the threshold? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why 0.5 is problematic | With 0.3% fraud rate, the model's calibrated probability for fraud might peak at 0.1 for true fraud cases. Using 0.5 misses all of them. |
| 2. How to find optimal threshold | Scan thresholds: `np.arange(0.01, 0.99, 0.01)`. For each, compute F1. Pick threshold maximizing F1 (or business-defined recall target). |
| 3. Lowering threshold | Increases recall (catch more positives) but decreases precision (more false alarms). |
| 4. Raising threshold | Decreases recall (miss more positives) but increases precision (fewer false alarms). |

</details>

---

## Exercise ID-13: Strategy Selection & Pipeline

| Question | Your Answer |
|----------|-------------|
| 1. For Mild imbalance (< 1:10), what strategies? | |
| 2. For Moderate imbalance (1:10–1:100), what strategies? | |
| 3. For Severe imbalance (> 1:100), what strategies? | |
| 4. Tabular data → preferred methods? | |
| 5. Text data → preferred methods? | |
| 6. Images → preferred methods? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Mild (< 1:10) | **class_weight='balanced'** + tune threshold |
| 2. Moderate (1:10–1:100) | **SMOTE + class_weight** + tune threshold |
| 3. Severe (> 1:100) | **SMOTE + RUS + class_weight** + tune threshold |
| 4. Tabular | **SMOTE-NC** (handles mixed numeric + categorical) |
| 5. Text | **class_weight only** (SMOTE doesn't work well on sparse text vectors) |
| 6. Images | **Focal Loss** (or data augmentation specific to images) |

</details>

---

## Exercise ID-14: Common Mistakes

| Question | Your Answer |
|----------|-------------|
| 1. Evaluating with Accuracy — problem and fix | |
| 2. Resampling the Test Set — problem and fix | |
| 3. Using sklearn Pipeline for SMOTE — problem and fix | |
| 4. Always Using 1:1 Ratio — problem and fix | |
| 5. SMOTE on Non-Tabular Data — problem and fix | |
| 6. Ignoring Threshold Optimization — problem and fix | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Evaluating with Accuracy | **Problem**: 99.7% accuracy but 0% recall. **Fix**: Use F1, PR-AUC, MCC, Recall as primary metrics. |
| 2. Resampling the Test Set | **Problem**: Test gets synthetic samples → invalid evaluation. **Fix**: Always use imblearn Pipeline which only resamples training folds. |
| 3. Using sklearn Pipeline for SMOTE | **Problem**: sklearn Pipeline does NOT apply transformers correctly during CV for resampling. **Fix**: Use `imblearn.pipeline.Pipeline` instead. |
| 4. Always Using 1:1 Ratio | **Problem**: 1:1 can be too aggressive. **Fix**: Treat balance ratio as a hyperparameter — cross-validate it. |
| 5. SMOTE on Non-Tabular Data | **Problem**: SMOTE interpolates assuming continuous numeric space; on text/images creates invalid samples. **Fix**: Use class_weight or data-type-specific augmentation. |
| 6. Ignoring Threshold Optimization | **Problem**: Default 0.5 threshold leaves recall very low. **Fix**: Always tune decision threshold on validation set using PR curve. |

</details>

---

# SECTION 2: SUPPORT VECTOR MACHINES

---

## Exercise SVM-1: Intuition — Maximum-Margin Classifier

| Question | Your Answer |
|----------|-------------|
| 1. What is the core idea of SVM? | |
| 2. What does "maximum margin" mean? | |
| 3. Why does wider margin lead to better generalization? | |
| 4. What is SVM great at? | |
| 5. Who introduced SVM and when? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Core idea | SVM finds the **widest separating line** — the one farthest from any training point on either side. |
| 2. Maximum margin | The margin is the distance between the decision boundary and the closest training points. SVM maximizes this distance. |
| 3. Why wider margin = better generalization | Wider margin → better generalization — the classifier is more robust to small changes in input. |
| 4. What SVM is great at | Small-N, high-D data (features > samples), clear margins, non-linear via kernel trick, convex problem (global optimum guaranteed). |
| 5. Introduced by | **Vapnik & Cortes (1995)**. Dominated ML competitions pre-deep-learning. |

</details>

---

## Exercise SVM-2: The Math — Hyperplanes & Margins

| Question | Your Answer |
|----------|-------------|
| 1. Write the hyperplane equation. | |
| 2. What is the decision rule for SVM? | |
| 3. What is the signed distance from a point to the hyperplane? | |
| 4. What is the scaling trick for SVM? | |
| 5. How does maximizing the margin relate to minimizing ||w||? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Hyperplane equation | **w · x + b = 0** (w, x ∈ ℝᵈ, b ∈ ℝ). w = weight vector (perpendicular to hyperplane), b = bias. |
| 2. Decision rule | **f(x) = sign(w · x + b)** — if w·x + b > 0 → predict +1; if < 0 → predict −1. |
| 3. Signed distance | **distance = (w · x + b) / \|w\|** |
| 4. Scaling trick | SVM chooses scale of w so support vectors satisfy w·x + b = ±1. With this choice, margin width = **2 / \|w\|** — so maximizing margin = minimizing \|w\|. |
| 5. Maximizing margin = minimizing \|w\| | Margin width = 2/\|w\|. Maximizing margin = maximizing 2/\|w\| = minimizing \|w\| = minimizing ½\|w\|². |

</details>

---

## Exercise SVM-3: Hard Margin Optimization

| Question | Your Answer |
|----------|-------------|
| 1. Write the hard margin SVM primal problem. | |
| 2. What are the constraints for hard margin? | |
| 3. Why is the optimization problem elegant? | |
| 4. What is the problem with hard margin? | |
| 5. When would hard margin fail? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Hard margin primal | **minimize ½\|w\|²** subject to **yᵢ(w·xᵢ + b) ≥ 1** for every training point i. |
| 2. Constraints | Every point must be on the correct side with margin ≥ 1. |
| 3. Why elegant | **Convex** → one global optimum (unlike neural nets). Efficient dual formulation reveals support vectors. |
| 4. Problem with hard margin | Requires **perfect separation**. Real-world data has noise and overlaps. |
| 5. When hard margin fails | Any mislabeled point or overlapping classes makes the problem infeasible (no solution). |

</details>

---

## Exercise SVM-4: Soft Margin & C Parameter

| Question | Your Answer |
|----------|-------------|
| 1. Write the soft margin SVM primal problem. | |
| 2. What are slack variables (ξᵢ)? | |
| 3. What does the C parameter control? | |
| 4. What happens with small C (e.g., 0.01)? | |
| 5. What happens with large C (e.g., 1000)? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Soft margin primal | **minimize ½\|w\|² + C Σ ξᵢ** subject to yᵢ(w·xᵢ+b) ≥ 1−ξᵢ, ξᵢ ≥ 0. |
| 2. Slack variables (ξᵢ) | ξᵢ = 0 → outside margin (OK). 0 < ξᵢ < 1 → inside margin. ξᵢ > 1 → misclassified. |
| 3. C parameter | Controls trade-off between **large margin** vs **few violations**. Larger C = less tolerance for margin violations. |
| 4. Small C (0.01) | Low penalty → soft margin. Wide margin, more slack. High bias, low variance → underfitting risk. Best for: noisy data, lots of overlap. |
| 5. Large C (1000) | High penalty → hard margin. Narrow margin, few slack. Low bias, high variance → overfitting risk. Best for: clean data, clear separation. |

</details>

---

## Exercise SVM-5: The Kernel Trick

| Question | Your Answer |
|----------|-------------|
| 1. Why do we need kernels for SVM? | |
| 2. What is the kernel trick? | |
| 3. What does Mercer's Theorem state? | |
| 4. Write the kernelized decision function. | |
| 5. Why is the kernel trick "magic"? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why kernels | Many datasets are not linearly separable. Need non-linear boundaries. Brute force feature expansion is computationally impossible (O(Dᵈ) features). |
| 2. Kernel trick | Replaces inner products x·x' with a kernel function K(x,x') that equals an inner product in a **high-dimensional space** — without computing the high-dimensional features. |
| 3. Mercer's Theorem | Any symmetric, positive semi-definite function K can serve as a valid kernel. Guarantees an (often implicit) feature map φ exists. |
| 4. Kernelized decision function | **f(x) = sign(Σ αᵢ yᵢ K(xᵢ, x) + b)** |
| 5. Why it's magic | Computing K(x,x') is often **cheap O(d)** — but it equals a dot product in **potentially infinite-dimensional space**. Expressiveness of high-D features, cost of working in original space. |

</details>

---

## Exercise SVM-6: Common Kernel Functions

| Question | Your Answer |
|----------|-------------|
| 1. Linear kernel — formula and best for | |
| 2. Polynomial kernel — formula and best for | |
| 3. RBF (Gaussian) kernel — formula and best for | |
| 4. Sigmoid kernel — formula and best for | |
| 5. Which kernel is the default choice? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Linear | **K = x·x'** — Best for: High-dim, sparse (text, genes). |
| 2. Polynomial | **K = (γ x·x' + r)ᵈ** — Best for: Interaction features; degree ≤ 5. |
| 3. RBF (Gaussian) | **K = exp(−γ \|x−x'\|²)** — **Default choice** for most data. Maps to infinite-dimensional space. |
| 4. Sigmoid | **K = tanh(γ x·x' + r)** — Neural-net style; rarely optimal. |
| 5. Default kernel | **RBF** — works well in practice. Use with `gamma='scale'`. |

</details>

---

## Exercise SVM-7: RBF Kernel — Gamma Parameter

| Question | Your Answer |
|----------|-------------|
| 1. What does γ (gamma) control in RBF kernel? | |
| 2. What happens with small γ (e.g., 0.01)? | |
| 3. What happens with large γ (e.g., 10)? | |
| 4. What is the effect of γ on bias/variance? | |
| 5. What does the RBF kernel's Taylor expansion reveal? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. γ controls | **Width of Gaussian bells**. Small γ = wide influence; large γ = narrow influence. |
| 2. Small γ (0.01) | Wide Gaussian bells — points influence each other over long distances. Smooth decision boundary. High bias, low variance → underfitting risk. Like a linear kernel. |
| 3. Large γ (10) | Narrow Gaussian bells — points only influence nearest neighbors. Complex, wiggly boundary. Low bias, high variance → overfitting risk. Like a nearest-neighbor classifier. |
| 4. Effect on bias/variance | Small γ = high bias, low variance. Large γ = low bias, high variance. |
| 5. Taylor expansion | Contains **infinitely many polynomial terms** — expressive power is enormous; can represent any smooth decision boundary given enough data. |

</details>

---

## Exercise SVM-8: Kernel Decision Guide

| Question | Your Answer |
|----------|-------------|
| 1. Text classification (sparse, high-D) → recommended kernel | |
| 2. Numeric features < 1,000 → recommended kernel | |
| 3. Known feature interactions (x × y matters) → recommended kernel | |
| 4. Very large N (> 100,000) → recommended kernel | |
| 5. Need interpretable weights → recommended kernel | |
| 6. First pass / unsure → recommended kernel | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Text classification | **Linear** — already effectively high-dimensional |
| 2. Numeric features < 1,000 | **RBF** — works on most tabular data; tune C and γ |
| 3. Known feature interactions | **Polynomial (degree 2–3)** — implicit interaction modeling |
| 4. Very large N (> 100,000) | **Linear + LinearSVC** — RBF scales O(N²)–O(N³); linear is near-linear in N |
| 5. Need interpretable weights | **Linear** — feature coefficients are directly interpretable |
| 6. First pass / unsure | **RBF** with γ='scale' — generally the best starting point |

</details>

---

## Exercise SVM-9: Support Vector Regression (SVR)

| Question | Your Answer |
|----------|-------------|
| 1. What is the core idea of SVR? | |
| 2. What is ε-insensitive loss? | |
| 3. Write the ε-insensitive loss function. | |
| 4. What are the knobs to tune in SVR? | |
| 5. How does SVR differ from MSE/MAE regression? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Core idea | Fits a function where predictions lie within an **ε-tube** around true values. Support vectors are points outside the tube. |
| 2. ε-insensitive loss | Errors smaller than ε → **no penalty**. Errors larger than ε → **linear penalty**. |
| 3. ε-insensitive loss | **L(y, f(x)) = max(0, \|y−f(x)\| − ε)** |
| 4. Knobs to tune | **ε** → tube width (noise tolerance). **C** → trade-off. **γ** → smoothness (for RBF SVR). |
| 5. Difference from MSE/MAE | MSE/MAE uses all points. SVR uses only points outside tube (~support vectors). Much sparser models, more robust to small noise. |

</details>

---

## Exercise SVM-10: SVM Strengths & Limitations

| Question | Your Answer |
|----------|-------------|
| 1. What are SVM strengths? | |
| 2. What are SVM limitations? | |
| 3. How does SVM scale with N? | |
| 4. Why is SVM sensitive to feature scaling? | |
| 5. Does SVM output calibrated probabilities natively? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Strengths | Effective in high dimensions (features >> samples), versatile via kernels, clear mathematical foundation (convex → global optimum), robust to overfitting, memory-efficient (only SVs stored), deterministic & reproducible. |
| 2. Limitations | Poor scaling with N (O(N²) to O(N³)), highly sensitive to scaling, no native probabilities (Platt scaling expensive and poorly calibrated), hyperparameter sensitivity (C and γ interact — grid search mandatory), multi-class is awkward (OvR/OvO), difficult to interpret (RBF/polynomial are black boxes). |
| 3. Scaling with N | Training is **O(N²) to O(N³)**. Becomes prohibitive for N > 100K. Use LinearSVC or switch to SGD/logistic regression. |
| 4. Sensitive to scaling | Unscaled features → one feature dominates distances → broken results. Always `StandardScaler` or `MinMaxScaler` first. |
| 5. Native probabilities | **No** — SVMs output distances, not calibrated probabilities. `probability=True` triggers expensive Platt scaling and often poorly calibrated. |

</details>

---

## Exercise SVM-11: Practical Tips & Checklist

| Question | Your Answer |
|----------|-------------|
| 1. What is the first step before SVM training? | |
| 2. What is the recommended starting kernel and parameter? | |
| 3. How to combine SVM with imbalance fixes? | |
| 4. What to use for large N (>50,000)? | |
| 5. What to benchmark SVM against? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. First step | **Always scale features** — `StandardScaler` (mean=0, std=1) inside a Pipeline. Never fit scaler on test data. |
| 2. Recommended starting point | `SVC(kernel='rbf', gamma='scale')`. Then grid search C and γ on log scales. Grid: C in [0.1, 1, 10, 100], γ in [0.001, 0.01, 0.1]. |
| 3. Combine with imbalance | `class_weight='balanced'` for class imbalance. SMOTE + SVM works well. Adjust decision threshold. |
| 4. Large N (>50,000) | `LinearSVC` (O(N)) or `SGDClassifier(loss='hinge')` for online training. |
| 5. Benchmark against | **Benchmark against LogReg and XGBoost first** — SVM shines for small-to-medium clean data with clear margins. |

</details>

---

# SECTION 3: MODEL EXPLAINABILITY & ERROR ANALYSIS

---

## Exercise ME-1: Why Explainability Matters

| Question | Your Answer |
|----------|-------------|
| 1. What is the "black-box problem"? | |
| 2. List the 6 reasons you need model explainability. | |
| 3. What is the solution to the black-box problem? | |
| 4. What is intrinsic (built-in) explainability? | |
| 5. What is post-hoc explainability? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Black-box problem | Modern ML models are often highly accurate but opaque. A random forest of 500 trees or a deep neural network has millions of parameters — we can't read their logic directly. |
| 2. Six reasons | **1. Trust & Adoption** — domain experts won't use what they don't understand. **2. Debug & Improve** — reveals why model fails. **3. Regulatory Compliance** — GDPR Article 22, US ECOA, EU AI Act. **4. Fairness & Ethics** — surfaces hidden bias. **5. Scientific Discovery** — reveals novel gene interactions, risk factors. **6. Stakeholder Communication** — translates model internals into business language. |
| 3. Solution | **Post-hoc explainability (SHAP, LIME)** — lets us enjoy the accuracy of black boxes while explaining their decisions. |
| 4. Intrinsic explainability | The model itself is transparent — you can read its logic directly. Examples: linear regression, decision trees, rule-based models, GAMs. **Pros**: perfect fidelity, fast, interpretable. **Cons**: often less accurate, can't explain existing black-box models. |
| 5. Post-hoc explainability | A separate layer explains an already-trained black-box model. Examples: SHAP, LIME, permutation importance, PDPs, counterfactuals. **Pros**: works with any model, keeps high-accuracy model. **Cons**: approximations (not 100% faithful), can disagree with each other, computationally expensive. |

</details>

---

## Exercise ME-2: Global vs Local Interpretability

| Question | Your Answer |
|----------|-------------|
| 1. What is global interpretability? | |
| 2. What is local interpretability? | |
| 3. Give an example question for global interpretability. | |
| 4. Give an example question for local interpretability. | |
| 5. Which scope do you use for auditing and reporting? | |
| 6. Which scope do you use for customer-facing explanations? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Global interpretability | Describes the model's behavior **overall** — across all predictions. Answers: "How does the model behave overall?" |
| 2. Local interpretability | Describes the model's behavior on a **single prediction**. Answers: "Why did the model make THIS particular prediction?" |
| 3. Global example | Across ALL 100,000 loan applications: credit score matters most (avg 42% of decision), then DTI (28%), then employment length (15%). |
| 4. Local example | For THIS applicant: DTI of 58% pushed denial strongly; credit score of 680 pushed slightly toward approval; income of $45K had near-zero effect. |
| 5. Auditing/reporting | **Global** — shows systematic issues, scientific discovery. |
| 6. Customer-facing | **Local** — explains specific predictions, regulatory appeals, debugging individual failures. |

</details>

---

## Exercise ME-3: Feature Importance — Built-In vs Permutation

| Question | Your Answer |
|----------|-------------|
| 1. What is Mean Decrease Impurity (MDI) importance? | |
| 2. What are the issues with MDI? | |
| 3. How does permutation importance work? | |
| 4. What are the advantages of permutation importance over MDI? | |
| 5. Which should you use for final results? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. MDI importance | Default for sklearn RandomForest. Sums the impurity decrease (Gini/entropy) each feature provides across all splits in all trees. |
| 2. Issues with MDI | Biased toward high-cardinality features, inflated for noisy continuous features, can't account for correlated features. MDI can rank a useless random feature as highly important! |
| 3. Permutation importance | Measures the drop in model performance when a feature's values are randomly shuffled. Algorithm: train model → compute baseline score → shuffle each feature → recompute score → importance = drop in performance. |
| 4. Advantages | Model-agnostic, no cardinality bias, uses held-out validation data (true generalization signal), includes uncertainty estimate (std across K shuffles). |
| 5. For final results | **Permutation importance** — use MDI for quick sanity check during training; always report permutation importance (on validation) for final results. |

</details>

---

## Exercise ME-4: Partial Dependence & ICE Plots

| Question | Your Answer |
|----------|-------------|
| 1. What does a Partial Dependence Plot (PDP) show? | |
| 2. What is the weakness of PDP? | |
| 3. What does an Individual Conditional Expectation (ICE) plot show? | |
| 4. What does ICE reveal that PDP hides? | |
| 5. When would you use PDP vs ICE? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. PDP shows | The **average model output** as one feature varies, holding all others fixed. Reveals monotonic vs non-monotonic relationships, threshold effects. |
| 2. Weakness of PDP | Averages can hide heterogeneity. Different subgroups may respond differently to the feature. |
| 3. ICE plot shows | Same idea, but **one line per individual** instead of averaging. Shows effect for each specific data point. |
| 4. ICE reveals | Heterogeneous effects across individuals, subgroups responding differently to the feature, interaction effects hiding inside PDP averages. |
| 5. PDP vs ICE | **PDP**: average effect across population. **ICE**: used when you suspect heterogeneity; usually shown together with PDP (mean line overlaid on ICE lines). |

</details>

---

## Exercise ME-5: SHAP Values — The Game-Theoretic Framework

| Question | Your Answer |
|----------|-------------|
| 1. What does SHAP stand for? | |
| 2. What is the Shapley value and who introduced it? | |
| 3. What are the four fairness axioms of Shapley values? | |
| 4. What is the local accuracy (efficiency) property? | |
| 5. What is the consistency property? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. SHAP stands for | **SHapley Additive exPlanations** |
| 2. Shapley value | Introduced by Lloyd Shapley (1953, Nobel Prize 2012). The unique way to fairly distribute a payout among players in a cooperative game, satisfying four fairness axioms simultaneously. |
| 3. Four fairness axioms | **Efficiency**: Sum of all SHAP values = prediction − baseline (full prediction accounted for). **Symmetry**: Features that contribute equally get equal credit. **Dummy**: A feature that doesn't change any prediction gets φ = 0. **Additivity**: SHAP values of an ensemble = weighted sum of each model's SHAPs. |
| 4. Local accuracy (Efficiency) | The explanation adds up to the prediction exactly: **Σ φᵢ + φ₀ = f(x)**. No missing attribution — every bit of the prediction is assigned to some feature. |
| 5. Consistency | If the model changes so that feature i contributes more (in every coalition), then φᵢ cannot decrease. **MDI fails this; permutation satisfies it.** |

</details>

---

## Exercise ME-6: SHAP Variants

| Question | Your Answer |
|----------|-------------|
| 1. TreeExplainer — model type, speed, exactness | |
| 2. LinearExplainer — model type, speed, exactness | |
| 3. DeepExplainer — model type, speed, exactness | |
| 4. KernelExplainer — model type, speed, exactness | |
| 5. Which explainer should you use for XGBoost? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. TreeExplainer | **Model**: Tree-based (XGBoost, RF, LGBM, CatBoost). **Speed**: Very fast (poly-time). **Exact**: Yes (exact). |
| 2. LinearExplainer | **Model**: Linear / logistic regression. **Speed**: Instant. **Exact**: Yes (exact). |
| 3. DeepExplainer | **Model**: Neural networks (PyTorch/TF). **Speed**: Fast. **Exact**: Approximation. |
| 4. KernelExplainer | **Model**: ANY model (model-agnostic fallback). **Speed**: Slow. **Exact**: Approximation (sampling). |
| 5. For XGBoost | **TreeExplainer** — fast and exact. |

</details>

---

## Exercise ME-7: SHAP Visualizations

| Question | Your Answer |
|----------|-------------|
| 1. Waterfall plot — what does it show and when to use? | |
| 2. Force plot — what does it show and when to use? | |
| 3. Summary bar plot — what does it show and when to use? | |
| 4. Beeswarm plot — what does it show and when to use? | |
| 5. Dependency plot — what does it show and when to use? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Waterfall plot | **Local interpretability**. Shows how each feature pushes the prediction from baseline to final value. Use for explaining individual predictions. |
| 2. Force plot | **Local interpretability**. Visual version of waterfall — features push prediction left (lower) or right (higher). Use for explaining individual predictions. |
| 3. Summary bar plot | **Global interpretability**. Shows mean absolute SHAP value per feature (average importance across all predictions). Use for global feature importance. |
| 4. Beeswarm plot | **Global interpretability**. Shows SHAP values by feature with color indicating feature value. Reveals direction (positive/negative) and distribution of impact. Use for global understanding of feature effects. |
| 5. Dependency plot | **Global interpretability**. Shows how SHAP value changes with feature value. Reveals non-linear relationships. Use to see effect shape (like PDP but with individual points). |

</details>

---

## Exercise ME-8: LIME — Local Interpretable Model-agnostic Explanations

| Question | Your Answer |
|----------|-------------|
| 1. What does LIME stand for? | |
| 2. How does LIME work? | |
| 3. What is the key insight behind LIME? | |
| 4. What is the important caveat of LIME? | |
| 5. LIME vs SHAP — which has theoretical guarantees? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. LIME stands for | **Local Interpretable Model-agnostic Explanations** (Ribeiro et al. 2016). |
| 2. How LIME works | Explains a single prediction by fitting a simple interpretable model (e.g., linear regression) to the black-box model's behavior in the **local neighborhood** of that prediction. |
| 3. Key insight | The black-box model may be non-linear globally, but in a small neighborhood around any point, it can usually be approximated by a simple linear model. |
| 4. Important caveat | The explanation is faithful only in that **local neighborhood**. Outside it, the linear approximation may be completely wrong. LIME does not provide global guarantees. |
| 5. Theoretical guarantees | **SHAP** has theoretical guarantees (game theory axioms). **LIME** is heuristic — no consistency guarantee, explanations can vary run-to-run. |

</details>

---

## Exercise ME-9: LIME vs SHAP — Choosing Between Them

| Question | LIME | SHAP |
|----------|------|------|
| 1. Theoretical basis | | |
| 2. Scope | | |
| 3. Additivity guarantee | | |
| 4. Consistency guarantee | | |
| 5. Stability (same input → same output) | | |
| 6. Speed on tree models | | |

<details>
<summary>📖 Click for Answers</summary>

| Question | LIME | SHAP |
|----------|------|------|
| 1. Theoretical basis | Local linear approximation (heuristic) | Game theory (Shapley values, axioms) |
| 2. Scope | Local only | Local + global (aggregates) |
| 3. Additivity guarantee | No | Yes (local accuracy property) |
| 4. Consistency guarantee | No — explanations can vary run-to-run | Yes |
| 5. Stability | Low — perturbations are random | High — deterministic |
| 6. Speed on tree models | Similar to KernelSHAP | Much faster via TreeExplainer |

**Rule of thumb**: Use SHAP by default for tabular models. Use LIME when you need quick per-sample explanations on exotic model types (custom text/image pipelines).

</details>

---

## Exercise ME-10: Systematic Error Analysis

| Question | Your Answer |
|----------|-------------|
| 1. Why is systematic error analysis important? | |
| 2. What does error analysis reveal? | |
| 3. What is the systematic error analysis workflow? | |
| 4. How does error analysis help with fairness? | |
| 5. What is the value of slicing errors? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why important | Your model has 89% accuracy. But **WHERE** are the 11% of errors? Error analysis reveals the structure in mistakes. |
| 2. Error analysis reveals | **Reveals Hidden Bias**: 94% for one group but 71% for another. **Prioritizes Fixes**: 60% of errors share one failure mode. **Drives Data Strategy**: errors on under-represented classes → collect more. **Guides Threshold Choice**: different subgroups may need different thresholds. **Detects Distribution Shift**: sudden rise in errors for a segment = drift. **Builds Stakeholder Trust**: "works well on these, unreliable on those" is more trustworthy. |
| 3. Workflow | **Step 1**: Separate correct vs errors (FP + FN). **Step 2**: Slice by demographic, feature value, time, location, class, or subgroup. **Step 3**: Quantify error rate per slice, compare to baseline, flag significant gaps. **Step 4**: Diagnose — SHAP per slice, check label quality, confusion patterns, manual inspection. **Step 5**: Fix — more training data, new features, different threshold, or different model per slice. **Step 6**: Monitor — log errors per slice, alert on drift, report on fairness. |
| 4. Fairness | Aggregate accuracy hides disparate impact — error slicing reveals it. Model may be 94% accurate for one group but 71% for another. |
| 5. Value of slicing | Reveals **structure in mistakes** — errors often cluster in specific segments. Fixing one failure mode can lift overall performance dramatically. |

</details>

---

## Exercise ME-11: Diagnosing Error Types

| Question | Your Answer |
|----------|-------------|
| 1. Label Noise — cause, detect, fix | |
| 2. Spurious Correlation — cause, detect, fix | |
| 3. Under-represented Subgroup — cause, detect, fix | |
| 4. Distribution Shift — cause, detect, fix | |
| 5. Ambiguous Ground Truth — cause, detect, fix | |
| 6. Feature Gap — cause, detect, fix | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Label Noise | **Cause**: training labels are wrong. **Detect**: examine errors manually; if you'd label them differently, it's label noise. **Fix**: clean labels, active learning, label smoothing. |
| 2. Spurious Correlation | **Cause**: model learned a shortcut (watermark, timestamp, background). **Detect**: SHAP shows a feature matters that shouldn't. **Fix**: remove feature, augment data, adversarial debiasing. |
| 3. Under-represented Subgroup | **Cause**: small slice ignored during training. **Detect**: error rate high on slice with low N. **Fix**: oversample / collect more data / class weights. |
| 4. Distribution Shift | **Cause**: production data differs from training. **Detect**: error rate rising over time; PSI/KS drift tests. **Fix**: retrain on recent data; continuous learning. |
| 5. Ambiguous Ground Truth | **Cause**: the task is inherently hard (even experts disagree). **Detect**: inter-annotator agreement is low. **Fix**: accept upper bound; use ensemble of expert labels. |
| 6. Feature Gap | **Cause**: missing the key predictive feature. **Detect**: errors cluster on a dimension not in features. **Fix**: feature engineering; collect new data source. |

</details>

---

## Exercise ME-12: Confusion Matrix Analysis

| Question | Your Answer |
|----------|-------------|
| 1. What does the diagonal of a confusion matrix show? | |
| 2. What do off-diagonal entries show? | |
| 3. For a clothing classifier, Shirt accuracy 58% and Dress accuracy 91% — what does this suggest? | |
| 4. Shirt ↔ T-shirt confusion (15%, 19%) — what does this suggest and what should you do? | |
| 5. Pullover ↔ Coat confusion (18%, 22%) — what does this suggest and what should you do? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Diagonal | Accuracy per class. Shows which classes the model handles well and which it struggles with. |
| 2. Off-diagonal | Shows which classes are confused with which. Specific confusions point to the underlying issue. |
| 3. Shirt 58% vs Dress 91% | Dress is easy (distinct shape). Shirt is hard (similar to other classes). Need more training data for shirts. |
| 4. Shirt ↔ T-shirt confusion | Shirts and T-shirts look similar — model struggles with similar silhouettes. **Action**: collect more training images of shirts; add a collar/sleeve detector feature. |
| 5. Pullover ↔ Coat confusion | Similar silhouette issue. **Action**: collect more examples of both; add texture/feature engineering to distinguish. |

</details>

---

## Exercise ME-13: Counterfactual Explanations

| Question | Your Answer |
|----------|-------------|
| 1. What is a counterfactual explanation? | |
| 2. Why are counterfactuals useful for customers? | |
| 3. Why are counterfactuals regulatory-friendly? | |
| 4. Give an example of a counterfactual for a loan denial. | |
| 5. How do counterfactuals compare to SHAP values for non-technical audiences? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Counterfactual explanation | Answers: **"What minimal change to the input would flip the model's prediction?"** — arguably the most actionable local explanation. |
| 2. Why useful for customers | Tells the person **what to DO** — specific, concrete change. Not just "your application was risky." |
| 3. Regulatory-friendly | GDPR Article 22 'right to explanation' is often interpreted as requiring counterfactuals for automated decisions. |
| 4. Loan denial example | Original: Denied (income=$45K, DTI=48%, credit_score=680). Counterfactual: Approved if DTI=35% instead of 48%. "If your DTI were 35% instead of 48%, your loan would be approved." |
| 5. Compared to SHAP | **Much clearer** than SHAP values for non-technical audiences. "Change X" is easier to understand than "feature attribution = 0.24." |

</details>

---

## Exercise ME-14: Production Error Monitoring Checklist

| Question | Your Answer |
|----------|-------------|
| 1. Log Every Prediction — why? | |
| 2. Monitor Subgroup Error Rates — how and why? | |
| 3. Track Feature Drift — what metric and threshold? | |
| 4. Sample for Manual Review — how many and why? | |
| 5. Version Control Everything — why? | |
| 6. Have a Rollback Plan — why? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Log Every Prediction | Store features, prediction, confidence, model version, and timestamp. Without logging, post-hoc analysis is impossible. |
| 2. Monitor Subgroup Error Rates | Dashboard: error rate per gender, age bucket, region, customer tier. Alert on any **2× worsening over baseline**. |
| 3. Track Feature Drift | **PSI (Population Stability Index)** per feature. PSI > 0.25 → significant drift; investigate immediately. |
| 4. Sample for Manual Review | Each week, review **20–50 misclassified cases** by hand. Humans notice patterns dashboards miss. |
| 5. Version Control Everything | Model, features, training data, labels. When errors spike, you need to know what changed. |
| 6. Have a Rollback Plan | If v2 errors are worse than v1, switch back in minutes. Shadow deployment + gradual rollout reduces risk. |

</details>

---

# 📊 COMPLETE COVERAGE SUMMARY

| Category | Concepts | Status |
|----------|----------|--------|
| Imbalanced Datasets | All major concepts | ✅ 100% |
| Support Vector Machines | All major concepts | ✅ 100% |
| Model Explainability & Error Analysis | All major concepts | ✅ 100% |
| **TOTAL** | **All Week 4 concepts** | ✅ **100%** |

---

## 📝 How to Use This Document

1. **Read the question**, write your answer in the blank/box
2. **Click the dropdown** to reveal the model answer
3. **Compare** your answer to the model
4. **Re-study** any sections where you got something wrong
5. **Mark** your confidence level for each topic

---

**Good luck with your exam! 🎯**