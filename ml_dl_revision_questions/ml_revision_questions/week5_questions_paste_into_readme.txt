# 📚 WEEK 5 — COMPLETE STUDY GUIDE
## All Exercises with Answers in Spoiler Format

---

# SECTION 1: DECISION TREES

---

## Exercise DT-1: Decision Tree Fundamentals

| Question | Your Answer |
|----------|-------------|
| 1. What is a decision tree? | |
| 2. What types of problems can decision trees solve? | |
| 3. What is the representation of a decision tree? | |
| 4. What is the expressivity of decision trees? | |
| 5. What are decision boundaries in decision trees? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What is a decision tree? | A hierarchical data structure that represents data by implementing a **divide and conquer strategy**. Can be used as a non-parametric classification and regression method. |
| 2. Types of problems | **Classification** (discrete categories) and **Regression** (real-valued outputs via regression trees). |
| 3. Representation | Nodes are **tests for feature values**. There is one branch for each value of the feature. Leaves specify the category (labels). |
| 4. Expressivity | As Boolean functions, they can represent **any Boolean function**. Can be rewritten as rules in **Disjunctive Normal Form (DNF)**. |
| 5. Decision boundaries | The tree divides the feature space into **axis-parallel rectangles**, each labeled with one of the labels. |

</details>

---

## Exercise DT-2: The ID3 Algorithm

| Question | Your Answer |
|----------|-------------|
| 1. What does ID3 stand for? | |
| 2. Describe the basic ID3 algorithm. | |
| 3. What is the main decision in the algorithm? | |
| 4. What is the goal when picking the root attribute? | |
| 5. Why can't we find the minimal decision tree efficiently? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. ID3 stands for | **Iterative Dichotomiser 3** — developed by Quinlan in the late 1970s. |
| 2. ID3 algorithm | Recursively build tree top-down: If all examples same label → return leaf. Else pick attribute that **best classifies** S (highest information gain). For each value v of A: create branch A=v, let S_v be subset with A=v, recursively call ID3(S_v, Attributes-{A}, Label). |
| 3. Main decision | The selection of the **next attribute to condition on** (which attribute best splits the data). |
| 4. Goal when picking root attribute | To have the resulting decision tree as **small as possible** (Occam's Razor). |
| 5. Why can't find minimal tree | Finding the minimal decision tree consistent with data is **NP-hard**. ID3 is a greedy heuristic search — cannot guarantee optimality. |

</details>

---

## Exercise DT-3: Entropy & Information Gain

| Question | Your Answer |
|----------|-------------|
| 1. Write the entropy formula for a binary classification. | |
| 2. What is entropy when all examples are of the same class? | |
| 3. What is entropy when classes are perfectly balanced (50/50)? | |
| 4. Write the information gain formula. | |
| 5. What does information gain measure? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Entropy formula | **H(S) = −p₊ log₂(p₊) − p₋ log₂(p₋)** where p₊ and p₋ are proportions of positive and negative examples. |
| 2. Entropy when all same class | **0** — no uncertainty (low entropy). |
| 3. Entropy when perfectly balanced | **1** — maximum uncertainty (high entropy). |
| 4. Information gain formula | **Gain(S, A) = H(S) − Σᵥ (|Sᵥ|/|S|) × H(Sᵥ)** where v are values of attribute A. |
| 5. What information gain measures | The **reduction in entropy** after splitting on attribute A. Higher gain = better attribute. |

</details>

---

## Exercise DT-4: Overfitting in Decision Trees

| Question | Your Answer |
|----------|-------------|
| 1. What is overfitting in decision trees? | |
| 2. What are the reasons for overfitting? | |
| 3. What is pruning? | |
| 4. What are the two approaches to avoiding overfitting? | |
| 5. What methods are used to evaluate subtrees for pruning? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Overfitting definition | A hypothesis h overfits if there is another hypothesis h' such that h has **smaller error on training data** but **larger error on test data** than h'. |
| 2. Reasons for overfitting | **Too much variance** in training data (not representative). **Too much noise** in training data (incorrect feature values or class labels). Result of minimizing empirical error with ability to do so. |
| 3. Pruning | **Remove leaves** and assign majority label of the parent to all items. Prune children of node s if all children are leaves and accuracy on validation set does not decrease. |
| 4. Two approaches | **Pre-pruning**: Stop growing tree early when not enough data. **Post-pruning**: Grow full tree, then remove nodes without sufficient evidence. |
| 5. Methods for pruning | **Cross-validation**: Reserve hold-out set to evaluate utility. **Statistical testing**: Test if regularity is chance. **Minimum Description Length**: Is additional complexity smaller than remembering exceptions? |

</details>

---

# SECTION 2: RANDOM FORESTS & BAGGING

---

## Exercise RF-1: Bagging Fundamentals

| Question | Your Answer |
|----------|-------------|
| 1. What does Bagging stand for? | |
| 2. How does the Bootstrap work? | |
| 3. How does Bagging work? | |
| 4. When does Bagging make sense? | |
| 5. What is the effect of Bagging on bias and variance? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Bagging stands for | **Bootstrap Aggregating** |
| 2. How Bootstrap works | Replicate dataset by **sampling with replacement**. Each bootstrap sample contains ~63% of original data (some observations appear multiple times, some not at all). |
| 3. How Bagging works | We apply a learning method to each bootstrap replicate to produce predictions f̂⁽¹⁾, ..., f̂⁽ᴮ⁾. Then **average the predictions**: f̂_bag(x) = (1/B) Σ f̂⁽ᵇ⁾(x). |
| 4. When Bagging makes sense | Reduces variance of prediction. Especially useful with **higher-variance / more flexible prediction methods** (e.g., decision trees). When n is large, bootstrap samples are like independent realizations of the data. |
| 5. Effect on bias and variance | **Reduces variance** (a large ensemble can't cause overfitting). **Bias is not changed** (much). |

</details>

---

## Exercise RF-2: Out-of-Bag (OOB) Error

| Question | Your Answer |
|----------|-------------|
| 1. What percentage of observations are used in each bootstrap sample? | |
| 2. What percentage are left out (OOB)? | |
| 3. How is OOB error computed? | |
| 4. What is OOB error equivalent to for large B? | |
| 5. Why is OOB error useful? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Percentage used | **~63%** of observations appear in each bootstrap sample (1 − 1/e ≈ 0.632). |
| 2. Percentage left out | **~37%** of observations are out-of-bag (not in the bootstrap sample). |
| 3. How OOB error is computed | For each sample xᵢ, find predictions ŷᵢᵇ for all bootstrap b which do NOT contain xᵢ (about 0.37B of them). Average to get ŷᵢᵒᵒᵇ. Compute error (yᵢ − ŷᵢᵒᵒᵇ)² and average over all observations. |
| 4. OOB equivalent to | For large B, OOB error is virtually equivalent to **LOOCV** (Leave-One-Out Cross-Validation). |
| 5. Why useful | Estimates test error **without** cross-validation (computationally expensive). No need for separate validation set. |

</details>

---

## Exercise RF-3: Random Forests

| Question | Your Answer |
|----------|-------------|
| 1. What is the weakness of Bagging that Random Forests address? | |
| 2. How do Random Forests differ from Bagging? | |
| 3. What is the default value of m (number of predictors to consider)? | |
| 4. How does Random Forests reduce correlation between trees? | |
| 5. Bagging trees = Random Forests with what m? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Weakness of Bagging | Trees produced by different bootstrap samples can be **very similar** — high correlation between predictions. |
| 2. How Random Forests differ | **Same as Bagging** (fit trees to bootstrap samples) PLUS **when growing the tree, select a random sample of m < p predictors** to consider at each branch. |
| 3. Default m value | **m ≈ √p** (square root of number of predictors) for classification. Can be tuned as a hyperparameter. |
| 4. How RF reduces correlation | Randomly selecting a subset of predictors at each split leads to **less similar trees** with **less correlated predictions**. |
| 5. Bagging trees = Random Forests with | **m = p** (consider all predictors at each split). |

</details>

---

## Exercise RF-4: Bagging vs Random Forests Comparison

| Question | Bagging | Random Forests |
|----------|---------|----------------|
| 1. Bootstrap samples? | | |
| 2. Predictors considered at each split? | | |
| 3. Correlation between trees? | | |
| 4. Test error compared? | | |
| 5. m parameter? | | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Bagging | Random Forests |
|----------|---------|----------------|
| 1. Bootstrap samples? | Yes | Yes |
| 2. Predictors considered at each split? | All p predictors | Random subset of m < p predictors |
| 3. Correlation between trees | High (trees are similar) | Low (trees are diverse) |
| 4. Test error compared | Higher | Lower (better generalization) |
| 5. m parameter? | m = p | m ≈ √p (default) |

</details>

---

# SECTION 3: BOOSTING

---

## Exercise BO-1: Boosting Fundamentals

| Question | Your Answer |
|----------|-------------|
| 1. What is the core idea of Boosting? | |
| 2. How does Boosting differ from Bagging? | |
| 3. What is the effect of Boosting on bias and variance? | |
| 4. What is the role of data re-weighting in Boosting? | |
| 5. What is the final prediction in Boosting? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Core idea | Combines the outputs of many **"weak" classifiers** to produce a powerful "committee". Learns multiple trees **sequentially**, each trying to improve upon its predecessor. |
| 2. How Boosting differs from Bagging | **Boosting**: Sequential, reduces bias, high dependency between ensemble elements, can overfit. **Bagging**: Parallel, reduces variance, low dependency, can't overfit. |
| 3. Effect on bias and variance | **Reduces bias** (a large ensemble can overfit). **Increases variance** (sequential dependence). |
| 4. Role of data re-weighting | Examples that were **misclassified by previous learners** get higher weight in the next iteration. Focuses on hard examples. |
| 5. Final prediction | **Weighted sum** of the individual classifiers: G(x) = Σ αₜ Gₜ(x) |

</details>

---

## Exercise BO-2: Gradient Boosted Decision Trees (GBDT)

| Question | Your Answer |
|----------|-------------|
| 1. What is the additive prediction model? | |
| 2. What is the objective function in GBDT? | |
| 3. What does the regularization term ω(fₜ) model? | |
| 4. How are new trees added sequentially? | |
| 5. What is the role of step-size (shrinkage/ε)? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Additive prediction model | **ŷᵢ = Σ fₜ(xᵢ)** where each fₜ is a decision tree. |
| 2. Objective function | **Obj = Σᵢ l(yᵢ, ŷᵢ) + Σₜ ω(fₜ)** where l is loss function and ω(fₜ) is regularization. |
| 3. Regularization term ω(fₜ) | Models the **complexity of the tree** — penalizes number of leaves, prevents overfitting. |
| 4. How new trees are added | Start from constant prediction, add a new decision tree fₜ each time: **ŷᵢ⁽ᵗ⁾ = ŷᵢ⁽ᵗ⁻¹⁾ + fₜ(xᵢ)**. |
| 5. Role of step-size (ε) | **Step-size (shrinkage)** usually set around 0.1. **Goal**: prevent overfitting. |

</details>

---

## Exercise BO-3: Taylor Expansion in GBDT

| Question | Your Answer |
|----------|-------------|
| 1. Why do we take Taylor expansion of the objective? | |
| 2. What are gᵢ and hᵢ? | |
| 3. How does the objective simplify after Taylor expansion? | |
| 4. Why is the simplification useful? | |
| 5. How does learning fₜ depend on the objective? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Why Taylor expansion? | To approximate the objective and make it easier to optimize. |
| 2. What are gᵢ and hᵢ? | **gᵢ = ∂_ŷᵢ l(yᵢ, ŷᵢ)** — first-order gradient (1st derivative). **hᵢ = ∂²_ŷᵢ l(yᵢ, ŷᵢ)** — second-order gradient (2nd derivative). |
| 3. Simplified objective | **Obj ≈ Σᵢ [gᵢ fₜ(xᵢ) + ½ hᵢ fₜ²(xᵢ)] + ω(fₜ)** — constants can be ignored for optimization. |
| 4. Why useful | Learning fₜ only depends on objective via **g and h**. We can directly learn trees that optimize the loss (rather than using heuristic procedure). |
| 5. How learning depends | Theoretical benefit: know what we're learning. Engineering benefit: can use any loss function by just computing g and h. |

</details>

---

## Exercise BO-4: Tree Definition & Scoring

| Question | Your Answer |
|----------|-------------|
| 1. How is a tree defined in GBDT? | |
| 2. What is the complexity of a tree? | |
| 3. What is the score of a tree? | |
| 4. What are the optimal weights for leaves? | |
| 5. What is the gain formula for adding a split? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Tree definition | Every leaf j has a weight wⱼ. For any data point in leaf j, predict wⱼ. q(x) indicates the leaf node that data point belongs to. |
| 2. Tree complexity | **ω(f) = γT + ½λΣ wⱼ²** where T = number of leaves, γ = cost of adding a leaf, λ = regularization. |
| 3. Score of a tree | **Score = −½ Σⱼ [Gⱼ² / (Hⱼ + λ)] + γT** where Gⱼ = Σ gᵢ and Hⱼ = Σ hᵢ for examples in leaf j. |
| 4. Optimal leaf weights | **wⱼ* = −Gⱼ / (Hⱼ + λ)** |
| 5. Gain formula for split | **Gain = ½ [G_L²/(H_L+λ) + G_R²/(H_R+λ) − (G_L+G_R)²/(H_L+H_R+λ)] − γ** where L and R are left/right children. |

</details>

---

## Exercise BO-5: Split Finding & Tree Growth

| Question | Your Answer |
|----------|-------------|
| 1. How does GBDT find the best split? | |
| 2. What is pre-stopping? | |
| 3. What is post-pruning? | |
| 4. Which is better: pre-stopping or post-pruning? | |
| 5. Why might a split with negative gain still be useful? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. How to find best split | For each node, enumerate over all features. For each feature, sort instances by feature value. Use linear scan to decide best split. Take best split across all features. |
| 2. Pre-stopping | Stop split if the best split has **negative gain**. Risk: maybe a split can benefit future splits. |
| 3. Post-pruning | Grow tree to **maximum depth**, then **recursively prune** all leaf splits with negative gain. Better than pre-stopping. |
| 4. Which is better | **Post-pruning** is generally better — avoids missing beneficial splits that would enable future good splits. |
| 5. Why negative gain might still be useful | A split with negative gain now might enable **future splits with positive gain** in children. Post-pruning handles this. |

</details>

---

## Exercise BO-6: XGBoost — System Optimizations

| Question | Your Answer |
|----------|-------------|
| 1. What does XGBoost stand for? | |
| 2. What are the system optimizations in XGBoost? | |
| 3. What is the block structure in XGBoost? | |
| 4. What is cache-aware access? | |
| 5. What is out-of-core computing? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. XGBoost stands for | **eXtreme Gradient Boosting** |
| 2. System optimizations | **Parallel tree construction** using column block structure. **Distributed Computing** for training on a cluster. **Out-of-Core Computing** for datasets that don't fit in memory. |
| 3. Block structure | Sorted structure for each feature — allows **linear scan** for split finding. Blocks can be distributed across machines or stored on disk. |
| 4. Cache-aware access | Prefetch gradient statistics into internal buffer. Allocate internal buffer for improved split finding. Reduces cache misses. |
| 5. Out-of-core computing | For datasets larger than memory. **CSC compression** by columns. **Block sharding** using multiple disks. |

</details>

---

## Exercise BO-7: XGBoost — Algorithm Features

| Question | Your Answer |
|----------|-------------|
| 1. What is the regularized objective in XGBoost? | |
| 2. What is shrinkage in XGBoost? | |
| 3. What is column subsampling? | |
| 4. What is sparsity-awareness? | |
| 5. What are the split finding options? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Regularized objective | **Loss + regularization** — penalizes number of leaves and leaf weights. Prevents overfitting. |
| 2. Shrinkage | **Step-size** (learning rate) applied to each tree. Prevents overfitting. |
| 3. Column subsampling | Randomly sample features at each split (like Random Forests). Reduces correlation between trees. |
| 4. Sparsity-awareness | Handles missing values efficiently. Learns optimal direction for missing values. |
| 5. Split finding options | **Exact** (global/local) and **Approximate** (global/local). Weighted quantile sketch for fast approximation. |

</details>

---

## Exercise BO-8: Boosting vs Bagging Summary

| Question | Boosting | Bagging |
|----------|----------|---------|
| 1. Training order | | |
| 2. Dependency between learners | | |
| 3. Effect on bias | | |
| 4. Effect on variance | | |
| 5. Risk | | |
| 6. Key goal | | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Boosting | Bagging |
|----------|----------|---------|
| 1. Training order | **Sequential** | **Parallel** |
| 2. Dependency between learners | **High** (each tries to fix previous errors) | **Low** (independent samples) |
| 3. Effect on bias | **Reduces bias** | Bias not changed (much) |
| 4. Effect on variance | **Increases variance** (can overfit) | **Reduces variance** (can't overfit) |
| 5. Risk | A large ensemble can **overfit** | A large ensemble **can't cause overfitting** |
| 6. Key goal | Combine weak learners to make strong learner | Average predictions to reduce variance |

</details>

---

## Exercise BO-9: History of Boosting

| Question | Your Answer |
|----------|-------------|
| 1. When was AdaBoost introduced? | |
| 2. When were Random Forests introduced? | |
| 3. When was Gradient Boosting Machine introduced? | |
| 4. What was the 1st Kaggle success for boosting? | |
| 5. How many winning solutions used XGBoost in 2015? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. AdaBoost introduced | **1996** |
| 2. Random Forests introduced | **1999** |
| 3. Gradient Boosting Machine introduced | **2001** |
| 4. 1st Kaggle success | **Higgs Boson Challenge** |
| 5. Winning solutions using XGBoost in 2015 | **17 out of 29** winning solutions |

</details>

---

# 📊 COMPLETE COVERAGE SUMMARY

| Category | Concepts | Status |
|----------|----------|--------|
| Decision Trees | All major concepts | ✅ 100% |
| Random Forests & Bagging | All major concepts | ✅ 100% |
| Boosting (GBDT, XGBoost) | All major concepts | ✅ 100% |
| **TOTAL** | **All Week 5 concepts** | ✅ **100%** |

---

## 📝 How to Use This Document

1. **Read the question**, write your answer in the blank/box
2. **Click the dropdown** to reveal the model answer
3. **Compare** your answer to the model
4. **Re-study** any sections where you got something wrong
5. **Mark** your confidence level for each topic

---

**Good luck with your exam! 🎯**