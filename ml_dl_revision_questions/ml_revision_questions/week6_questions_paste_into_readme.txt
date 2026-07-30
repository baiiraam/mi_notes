# 📚 WEEK 6 — COMPLETE STUDY GUIDE
## All Exercises with Answers in Spoiler Format

---

# SECTION 1: DIMENSIONALITY REDUCTION

---

## Exercise DR-1: Motivation & Overview

| Question | Your Answer |
|----------|-------------|
| 1. What is dimensionality reduction? | |
| 2. Why do we need dimensionality reduction? | |
| 3. What is the goal of dimensionality reduction? | |
| 4. What are the three main approaches to dimensionality reduction? | |
| 5. What is representation learning? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Dimensionality reduction | Map data to a **lower-dimensional space** while preserving important structure. |
| 2. Why we need it | **Save computation/memory**. **Reduce overfitting**, achieve better generalization. **Visualize** in 2 or 3 dimensions. Mitigate the **curse of dimensionality**. |
| 3. Goal | Find a low-dimensional representation that captures the essential structure of the data. |
| 4. Three main approaches | **Distance preservation**, **Topology preservation**, **Information preservation**. |
| 5. Representation learning | Learning a mapping to a space that's easier to manipulate or visualize. Mapping data to a low-dimensional space is called **dimensionality reduction**. |

</details>

---

## Exercise DR-2: PCA — Overview & Projection

| Question | Your Answer |
|----------|-------------|
| 1. What does PCA stand for? | |
| 2. Is PCA a linear or non-linear method? | |
| 3. What is the projection of a point onto a subspace? | |
| 4. What is the reconstruction of a point? | |
| 5. What is the code/representation of a point? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. PCA stands for | **Principal Component Analysis** |
| 2. Linear or non-linear? | **Linear** — the mapping is a projection. |
| 3. Projection onto a subspace | Projₛ(x) = **x̂** = **Uz** where **z** = **Uᵀx** and **U** is a D×K matrix with orthonormal columns. |
| 4. Reconstruction | **x̂** = **µ** + **Uz** where **µ** is the empirical mean. The reconstructed point in the original space. |
| 5. Code/representation | **z** = **Uᵀ(x − µ)** — the low-dimensional representation of the data point. |

</details>

---

## Exercise DR-3: PCA — Learning the Subspace

| Question | Your Answer |
|----------|-------------|
| 1. What are the two equivalent criteria for PCA? | |
| 2. What is the reconstruction error criterion? | |
| 3. What is the projected variance criterion? | |
| 4. How are the two criteria related? | |
| 5. What does the Pythagorean Theorem tell us about PCA? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Two equivalent criteria | **Minimize reconstruction error** OR **Maximize projected variance**. They are equivalent! |
| 2. Reconstruction error | **Minimize (1/n) Σᵢ ‖xᵢ − x̂ᵢ‖²** — find subspace where data is reconstructed most accurately. |
| 3. Projected variance | **Maximize (1/n) Σᵢ ‖zᵢ − mean(z)‖²** — find subspace where data has the most variability. |
| 4. How they relate | **Projected variance = constant − reconstruction error**. Maximizing variance ≡ minimizing reconstruction error. |
| 5. Pythagorean Theorem | For any point: **‖x − µ‖² = ‖projection‖² + ‖residual‖²**. Total variance = projected variance + reconstruction error. |

</details>

---

## Exercise DR-4: PCA — The Solution

| Question | Your Answer |
|----------|-------------|
| 1. What is the empirical covariance matrix? | |
| 2. What are the principal components of PCA? | |
| 3. For K=1, what is the optimal PCA direction? | |
| 4. For general K, what is the optimal PCA subspace? | |
| 5. Why are principal components analogous to ellipse axes? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Empirical covariance matrix | **Σ̂ = (1/n) Σᵢ (xᵢ − µ)(xᵢ − µ)ᵀ** — symmetric and positive semidefinite. |
| 2. Principal components | The **top K eigenvectors** of the empirical covariance matrix Σ̂. |
| 3. For K=1 | The optimal PCA direction is the **top eigenvector** of Σ̂ (the direction of maximum variance). |
| 4. For general K | The optimal PCA subspace is spanned by the **top K eigenvectors** of Σ̂. |
| 5. Analogy to ellipse axes | Principal components are analogous to the principal axes of an ellipse — the directions of greatest spread. |

</details>

---

## Exercise DR-5: PCA — Applications

| Question | Your Answer |
|----------|-------------|
| 1. What are "eigenfaces"? | |
| 2. How many components are needed for good face reconstructions? | |
| 3. What is PCA used for in face recognition? | |
| 4. What is PCA used for in visualization? | |
| 5. How does PCA help with the curse of dimensionality? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Eigenfaces | The principal components of face images. They represent the main modes of variation in faces (lighting, expression, identity). |
| 2. Components for good reconstruction | **Only 3 components** can give good reconstructions of 19×19 (361-dimensional) grayscale images. |
| 3. PCA for face recognition | Apply classifier to the **latent representation** (low-dimensional code) — reduces overfitting and improves accuracy. |
| 4. PCA for visualization | Projects high-dimensional data to 2D or 3D for visualization (e.g., house area vs price shows linear relationship). |
| 5. Curse of dimensionality | Reduces feature dimension → less overfitting, faster computation, and better generalization. |

</details>

---

## Exercise DR-6: t-SNE — Overview

| Question | Your Answer |
|----------|-------------|
| 1. What does t-SNE stand for? | |
| 2. What is t-SNE specialized for? | |
| 3. What is the key idea of SNE? | |
| 4. What does t-SNE aim to preserve? | |
| 5. How does t-SNE differ from PCA? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. t-SNE stands for | **t-Distributed Stochastic Neighbor Embedding** |
| 2. What t-SNE is specialized for | **Visualization** — maps high-dimensional data to 2D/3D while preserving structure. |
| 3. Key idea of SNE | Converts Euclidean distances to **similarities** that can be interpreted as **probabilities** (Stochastic Neighbor Embedding). |
| 4. What t-SNE preserves | **Local structure** — similar points in high-D should be close in low-D. Focuses on topology preservation (neighborhood relationships). |
| 5. How t-SNE differs from PCA | **PCA** is linear, preserves global variance, fast. **t-SNE** is non-linear, preserves local topology, slower, specialized for visualization. |

</details>

---

## Exercise DR-7: t-SNE — Pairwise Similarities

| Question | Your Answer |
|----------|-------------|
| 1. How does t-SNE compute pairwise similarities in high-D? | |
| 2. How does t-SNE compute pairwise similarities in low-D? | |
| 3. What is perplexity in t-SNE? | |
| 4. What does perplexity control? | |
| 5. What is the typical range for perplexity? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. High-D similarities | **pⱼ|ᵢ = exp(−‖xᵢ−xⱼ‖² / 2σᵢ²) / Σₖ exp(−‖xᵢ−xₖ‖² / 2σᵢ²)** — Gaussian centered at each point. |
| 2. Low-D similarities | **qⱼ|ᵢ = (1 + ‖yᵢ−yⱼ‖²)⁻¹ / Σₖ (1 + ‖yᵢ−yₖ‖²)⁻¹** — Student-t distribution (heavier tails). |
| 3. Perplexity | A smooth measure of the **effective number of neighbors** for each point. Perp(P) = 2ᴴ⁽ᴾ⁾ where H(P) is entropy. |
| 4. What perplexity controls | Controls the **balance** between local and global structure. Low perplexity → focus on very local structure. High perplexity → more global structure. |
| 5. Typical perplexity range | **5–50** (commonly 30). |

</details>

---

## Exercise DR-8: t-SNE — Cost Function & Challenges

| Question | Your Answer |
|----------|-------------|
| 1. What is the cost function of t-SNE? | |
| 2. Why use KL divergence? | |
| 3. Why does t-SNE use Student-t distribution in low-D? | |
| 4. What is the "crowding problem"? | |
| 5. How does t-SNE optimize the cost function? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Cost function | **C = Σᵢ KL(Pᵢ || Qᵢ) = Σᵢ Σⱼ pⱼ|ᵢ log(pⱼ|ᵢ / qⱼ|ᵢ)** — sum of KL divergences for each point's neighborhood distribution. |
| 2. Why KL divergence | Measures the **faithfulness** with which qⱼ|ᵢ models pⱼ|ᵢ. Always positive. Asymmetric (focuses on preserving local structure). |
| 3. Why Student-t in low-D | **Heavier tails** compensate for the "crowding problem" — gives more space in low-D to separate points. |
| 4. Crowding problem | There is much more space in high dimensions than in low dimensions. Many points that are far apart in high-D can't be placed far enough apart in low-D. |
| 5. Optimization | **Gradient descent** + Momentum + Adaptive learning rate. Non-convex optimization. Tricks: Early Compression, Early Exaggeration. |

</details>

---

## Exercise DR-9: t-SNE — Applications

| Question | Your Answer |
|----------|-------------|
| 1. What is t-SNE used for in NLP? | |
| 2. What is t-SNE used for in computer vision? | |
| 3. How does t-SNE help with representation learning? | |
| 4. Why is t-SNE popular for visualizing learned representations? | |
| 5. What is a key limitation of t-SNE? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. t-SNE in NLP | **Word embeddings** — visualizes semantic and syntactic similarity. Words with similar meanings cluster together. |
| 2. t-SNE in computer vision | **Image embeddings** — visualizes how CNN representations separate different classes. |
| 3. Representation learning | t-SNE can be used to **make sense of learned representations** — visualize what the model has learned. |
| 4. Why popular for visualization | Provides **intuitive 2D/3D plots** that reveal clusters and structure in data. Has gained a lot of popularity for data exploration. |
| 5. Key limitation | **Stochastic** — different runs may give different results. Cannot be used for out-of-sample extension (new points must be embedded with existing points). |

</details>

---

# SECTION 2: DENSITY ESTIMATION

---

## Exercise DE-1: Kernel Density Estimation — Fundamentals

| Question | Your Answer |
|----------|-------------|
| 1. What is a kernel density estimate (KDE)? | |
| 2. Write the KDE formula. | |
| 3. What are the properties of a kernel function? | |
| 4. What does the bandwidth h control? | |
| 5. What happens when h is too small? Too large? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What is KDE | A non-parametric way to estimate the probability density function of a random variable. Places a kernel function on every data point and averages them. |
| 2. KDE formula | **f̂(x) = (1/(nh)) Σᵢ K((x − xᵢ)/h)** where K is the kernel function, h is the bandwidth. |
| 3. Kernel properties | **Non-negative**: K(x) ≥ 0. **Symmetric**: K(x) = K(−x). **Decreasing**: K'(x) ≤ 0 for x > 0. |
| 4. Bandwidth h controls | The **smoothness** of the density estimate. Larger h = smoother (more bias). Smaller h = more wiggly (more variance). |
| 5. h too small vs too large | **Too small**: under-smoothing — many spikes, high variance, overfitting. **Too large**: over-smoothing — loses detail, high bias, underfitting. |

</details>

---

## Exercise DE-2: Common Kernel Functions

| Question | Your Answer |
|----------|-------------|
| 1. What is the Gaussian kernel? | |
| 2. What is the Triangular (Linear) kernel? | |
| 3. What is the Box kernel? | |
| 4. What is the Triweight kernel? | |
| 5. Which kernel is most commonly used? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Gaussian kernel | **K(x) = (1/√(2π)) exp(−x²/2)** — smooth, infinitely differentiable, most commonly used. |
| 2. Triangular (Linear) kernel | **f(x) ∝ max(1 − |x|, 0)** — piecewise linear, finite support. |
| 3. Box kernel | **K(x) ∝ 1 for |x| ≤ 1, 0 otherwise** — simplest, produces step-like estimate. |
| 4. Triweight kernel | **K(x) ∝ (1 − x²)³ for |x| ≤ 1** — very smooth, finite support. |
| 5. Most commonly used | **Gaussian kernel** — smooth and well-behaved. |

</details>

---

## Exercise DE-3: Bandwidth Selection

| Question | Your Answer |
|----------|-------------|
| 1. What is Silverman's rule of thumb? | |
| 2. What assumption does Silverman's rule make? | |
| 3. What is the Improved Sheather Jones (ISJ) algorithm? | |
| 4. Why is ISJ more robust than Silverman? | |
| 5. What is the bias-variance tradeoff in KDE? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Silverman's rule of thumb | Computes an **optimal h** by assuming the data is normally distributed: **h ≈ 1.06 × σ × n⁻¹/⁵** (for Gaussian kernel). |
| 2. Assumption | Assumes data is **normally distributed** — good starting point in many cases but can fail for multimodal data. |
| 3. ISJ algorithm | More robust bandwidth selection method. Works better for **multimodal** data. |
| 4. Why ISJ is more robust | Handles **multimodality** better than Silverman. Doesn't assume normality. |
| 5. Bias-variance tradeoff | **Small h**: low bias, high variance (wiggly). **Large h**: high bias, low variance (smooth). Optimal h balances bias and variance. |

</details>

---

## Exercise DE-4: Weighted Data in KDE

| Question | Your Answer |
|----------|-------------|
| 1. How do we add weights to data points in KDE? | |
| 2. Write the weighted KDE formula. | |
| 3. Why might we want to weight data points? | |
| 4. What happens to the KDE with unequal weights? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Weighted KDE | Add weights wᵢ to data points xᵢ in the KDE formula. |
| 2. Weighted KDE formula | **f̂(x) = (1/(Σ wᵢ)) Σᵢ wᵢ × (1/h) K((x − xᵢ)/h)** |
| 3. Why weight data | To give more importance to certain data points (e.g., in bootstrapping, importance sampling, or with uneven sampling). |
| 4. Effect of unequal weights | Points with higher weights contribute more to the density estimate. |

</details>

---

# SECTION 3: CLUSTERING

---

## Exercise CL-1: Clustering Fundamentals

| Question | Your Answer |
|----------|-------------|
| 1. What is clustering? | |
| 2. What type of learning is clustering? | |
| 3. What is the goal of clustering? | |
| 4. What are the three clustering algorithms we covered? | |
| 5. What is a key difference between clustering and classification? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Clustering | Assigning observations to groups when we do not have class labels (Y). |
| 2. Type of learning | **Unsupervised learning** — no clearly defined outcome of interest. |
| 3. Goal | Find **homogeneous subgroups** among the observations. |
| 4. Three algorithms | **K-means clustering**, **Hierarchical clustering**, **Expectation Maximization (GMMs)** . |
| 5. Key difference | **Classification**: supervised (have labels Y). **Clustering**: unsupervised (no labels). |

</details>

---

## Exercise CL-2: K-Means Clustering

| Question | Your Answer |
|----------|-------------|
| 1. How many clusters must be specified in K-means? | |
| 2. What is the objective of K-means? | |
| 3. Describe the K-means algorithm steps. | |
| 4. Does K-means always converge to the global minimum? | |
| 5. Why is K-means random? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Number of clusters | **K must be specified a-priori**. |
| 2. Objective | Minimize **within-cluster variation**: minimize Σⱼ Σᵢ∈Cⱼ D²(xᵢ, μⱼ) where μⱼ is the centroid (mean) of cluster j. |
| 3. Algorithm steps | **Step 1**: Assign each observation randomly to one of K clusters. **Step 2a**: Find the centroid of each of K clusters. **Step 2b**: Reassign each sample to the nearest centroid (using Euclidean distance). Repeat until cluster assignments stop changing. |
| 4. Convergence | Always converges to a **local minimum** (not necessarily global). |
| 5. Randomness | Each initialization can result in a different minimum. Can run with multiple initializations and select the lowest minimum. |

</details>

---

## Exercise CL-3: Hierarchical Clustering

| Question | Your Answer |
|----------|-------------|
| 1. What does hierarchical clustering produce? | |
| 2. Does hierarchical clustering require specifying K a-priori? | |
| 3. What type of hierarchical clustering is most common? | |
| 4. How are clusters created in hierarchical clustering? | |
| 5. What is a dendrogram? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. What it produces | A **dendrogram** — a tree-like structure showing nested clusters. |
| 2. Does it require K? | **No** — the number of clusters does not need to be specified a-priori. |
| 3. Most common type | **Agglomerative** (bottom-up) — start with each point as its own cluster, iteratively fuse closest clusters. |
| 4. How clusters are created | In each iteration, fuse the **2 clusters closest** to each other. Cut the dendrogram at a vertical point to get K clusters. |
| 5. Dendrogram | Tree diagram showing the hierarchical relationship between clusters. Lower clusters are nested within higher clusters. |

</details>

---

## Exercise CL-4: Linkage Methods

| Question | Your Answer |
|----------|-------------|
| 1. What does linkage define? | |
| 2. How does Complete Linkage work? | |
| 3. How does Average Linkage work? | |
| 4. How does Single Linkage work? | |
| 5. How does Centroid Linkage work? | |
| 6. What is the "chaining phenomenon"? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Linkage | Defines the **dissimilarity between two clusters** when they contain multiple observations. |
| 2. Complete Linkage | Distance between two clusters = **maximum distance** between any pair of samples, one in each cluster. |
| 3. Average Linkage | Distance between two clusters = **average of all pairwise distances** between samples in the two clusters. |
| 4. Single Linkage | Distance between two clusters = **minimum distance** between any pair of samples, one in each cluster. Suffers from **chaining phenomenon**. |
| 5. Centroid Linkage | Distance between two clusters = **distance between each centroid**. Suffers from **inversions**. |
| 6. Chaining phenomenon | Single linkage tends to produce long, "chain-like" clusters because it only considers the closest pair. |

</details>

---

## Exercise CL-5: Clustering — Questions & Choices

| Question | Your Answer |
|----------|-------------|
| 1. Is clustering always appropriate? | |
| 2. How do we choose the number of clusters? | |
| 3. How do we test if clusters are robust? | |
| 4. Should we scale variables before clustering? | |
| 5. Does Euclidean distance always capture dissimilarity? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Is clustering always appropriate? | **Not always** — consider if a sample could belong to more than one cluster (use mixture models, soft clustering, topic models). |
| 2. Choosing number of clusters | **Subjective** — depends on inference sought. Some formal methods: gap statistics, mixture models, etc. |
| 3. Testing robustness | Run clustering on different **random subsets** of data — is the structure preserved? Try different clustering algorithms — are conclusions consistent? **Temper your conclusions.** |
| 4. Scaling variables | Variables with larger variance have a larger effect on Euclidean distance. Should consider **scaling** before clustering. |
| 5. Euclidean distance | Not always appropriate. For market segmentation, **correlation distance** may better capture customers who purchase **similar** things (rather than similar quantities). |

</details>

---

## Exercise CL-6: Correlation Distance

| Question | Your Answer |
|----------|-------------|
| 1. What problem does correlation distance solve? | |
| 2. What does correlation distance measure? | |
| 3. When would you use correlation distance instead of Euclidean? | |
| 4. Give an example of when correlation distance is more appropriate. | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Problem solved | Euclidean distance clusters customers who purchase similar **quantities**. Correlation distance clusters customers who purchase **similar patterns** across products. |
| 2. What it measures | The **correlation** between two observations across features — captures similarity in **shape/pattern** rather than magnitude. |
| 3. When to use | When we care about **purchase patterns** rather than total volume. When variables have different scales. |
| 4. Example | Market segmentation: Euclidean would cluster all customers who purchase few things together. Correlation would cluster customers who purchase **similar types** of things together (e.g., both buy more of product A than product B). |

</details>

---

# SECTION 4: GAUSSIAN MIXTURE MODELS (GMMs)

---

## Exercise GMM-1: Generative View of Clustering

| Question | Your Answer |
|----------|-------------|
| 1. What is a generative model for clustering? | |
| 2. What is the generative process for a GMM? | |
| 3. What are the parameters of a GMM? | |
| 4. What is the marginal distribution p(x) in a GMM? | |
| 5. What is a "responsibility" in GMM? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Generative model | Imagine data was produced by a model. Adjust model parameters using maximum likelihood to maximize probability of producing exactly the observed data. |
| 2. Generative process | **Step 1**: Choose a cluster z ∈ {1, ..., K} with probability p(z=k) = πₖ. **Step 2**: Given z, sample x from a Gaussian: p(x\|z=k) = N(x\|µₖ, Σₖ). |
| 3. Parameters | **πₖ** (mixing coefficients), **µₖ** (means), **Σₖ** (covariances). For simplicity, often assume Σₖ = I. |
| 4. Marginal distribution | **p(x) = Σᵢ πᵢ N(x\|µᵢ, Σᵢ)** — a Gaussian Mixture Model (GMM). GMMs are universal approximators of densities (with enough Gaussians). |
| 5. Responsibility | **rₙₖ = p(zₙ = k \| xₙ)** — the probability that cluster k generated data point n. Computed using Bayes rule. |

</details>

---

## Exercise GMM-2: Maximum Likelihood for GMMs

| Question | Your Answer |
|----------|-------------|
| 1. What is the maximum likelihood objective for GMMs? | |
| 2. Why is the objective difficult to optimize? | |
| 3. What would make the optimization easy? | |
| 4. What is the complete data log-likelihood? | |
| 5. How do we deal with unobserved cluster assignments? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. ML objective | **Maximize log p(X) = Σₙ log [Σₖ πₖ N(xₙ\|µₖ, Σₖ)]** |
| 2. Why difficult | **No closed form** solution when setting derivatives to zero. **Difficult** because sum is inside the log. |
| 3. What would make it easy | If we knew the **cluster assignments zₙ** for every data point. |
| 4. Complete data log-likelihood | **log p(X,Z) = Σₙ Σₖ I[zₙ=k] [log πₖ + log N(xₙ\|µₖ, Σₖ)]** |
| 5. Dealing with unobserved assignments | Replace I[zₙ=k] with its **expectation** under p(zₙ\|xₙ): **rₙₖ = E[I[zₙ=k]\|xₙ] = p(zₙ=k\|xₙ)** |

</details>

---

## Exercise GMM-3: EM Algorithm for GMMs

| Question | Your Answer |
|----------|-------------|
| 1. What does EM stand for? | |
| 2. What are the two steps of EM? | |
| 3. What happens in the E-step? | |
| 4. What happens in the M-step? | |
| 5. How do we check for convergence? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. EM stands for | **Expectation-Maximization** |
| 2. Two steps | **E-step** and **M-step** — alternate until convergence. |
| 3. E-step | Compute **responsibilities rₙₖ = p(zₙ=k\|xₙ)** given current model parameters (πₖ, µₖ, Σₖ). |
| 4. M-step | Re-estimate parameters **given current responsibilities** rₙₖ. πₖ = (1/n) Σₙ rₙₖ, µₖ = (Σₙ rₙₖ xₙ) / (Σₙ rₙₖ). |
| 5. Convergence check | Evaluate **log likelihood** and check for convergence. EM guarantees the likelihood does not decrease at each iteration. |

</details>

---

## Exercise GMM-4: GMM — Further Discussion

| Question | Your Answer |
|----------|-------------|
| 1. What assumption did we make for simplicity? | |
| 2. What happens if we remove this assumption? | |
| 3. What are possible problems with maximum likelihood for GMMs? | |
| 4. Is EM convex or non-convex? | |
| 5. What are mixture models more generally? | |

<details>
<summary>📖 Click for Answers</summary>

| Question | Answer |
|----------|--------|
| 1. Simplifying assumption | Assumed **Σₖ = I** (all clusters have identity covariance). |
| 2. Removing the assumption | Allows clusters to have **different spatial extents**. Algorithm remains very simple (full covariance GMMs). |
| 3. Problems with ML | **Singularities**: Arbitrarily large likelihood when a Gaussian explains a single point with variance shrinking to zero. **Non-convex** objective. |
| 4. EM non-convex | EM is **non-convex** — different initializations can lead to different local optima. |
| 5. Mixture models | Very powerful models — **universal distribution approximators**. Can replace Gaussian with other distributions (continuous or discrete). |

</details>

---

## Exercise GMM-5: K-means vs GMMs

| Question | K-means | GMMs |
|----------|---------|------|
| 1. Hard or soft assignment? | | |
| 2. Requires K a-priori? | | |
| 3. Assumes covariance? | | |
| 4. Provides probabilities? | | |
| 5. Type of clustering? | | |

<details>
<summary>📖 Click for Answers</summary>

| Question | K-means | GMMs |
|----------|---------|------|
| 1. Hard or soft assignment? | **Hard** (each point belongs to exactly one cluster) | **Soft** (points have probabilities/ responsibilities for each cluster) |
| 2. Requires K a-priori? | Yes (specified in advance) | Yes (specified in advance) |
| 3. Assumes covariance? | Spherical clusters (implicit) | Can have different covariance matrices (full covariance) |
| 4. Provides probabilities? | No | Yes (responsibilities and density estimates) |
| 5. Type of clustering? | Geometric | Probabilistic (generative) |

</details>

---

# 📊 COMPLETE COVERAGE SUMMARY

| Category | Concepts | Status |
|----------|----------|--------|
| Dimensionality Reduction (PCA, t-SNE) | All major concepts | ✅ 100% |
| Density Estimation (KDE) | All major concepts | ✅ 100% |
| Clustering (K-means, Hierarchical, GMMs) | All major concepts | ✅ 100% |
| **TOTAL** | **All Week 6 concepts** | ✅ **100%** |

---

## 📝 How to Use This Document

1. **Read the question**, write your answer in the blank/box
2. **Click the dropdown** to reveal the model answer
3. **Compare** your answer to the model
4. **Re-study** any sections where you got something wrong
5. **Mark** your confidence level for each topic

---

**Good luck with your exam! 🎯**