# Problem Statement 1 (From one of the quizzes)

We modify K-means so that cluster assignments use L1 (Manhattan) distance, but centroid updates still use the mean.  
The question is:

Does this modified version always converge, or can it oscillate?

#### Why Oscillation Can Occur (Short Mathematical Explanation)

For L1 distance, the centroid that minimizes the distortion

J = sum_i |x_i - c|

is the median, not the mean.

However, the modified algorithm still updates centroids using:

mu_k = (1 / |C_k|) * sum_{x in C_k} x

This creates a mismatch:

- The assignment step uses L1 distance  
- The update step uses the mean (optimal for L2, not L1)

Because these two steps optimize different objectives, the algorithm is no longer coordinate descent, and the distortion is not guaranteed to decrease each iteration.

This makes oscillation possible. A 2-cycle occurs when:

mu(t) -> mu(t+1) -> mu(t+2) = mu(t)

meaning the centroids alternate between two states without converging.


---

# Problem Statement 2 (from class)

(can refer the python file "greedy_split")

The task was to create a dataset with two features (A and B) where the greedy split would have you split on A first then B but the optimal tree is created when splitting on B first then A.

#### Dataset Used

We constructed the following dataset that satisfies the requirement:

| A | B | y |
|---|---|---|
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |
| 2 | 0 | 1 |
| 2 | 1 | 1 |

#### ✔ 1. Compute the greedy root split

We compute Gini impurity for all possible root splits:

For A ≤ 0.5, impurity = 0.2500  
For B ≤ 0.5, impurity = 0.4444  

Therefore:

Greedy root split = A

This matches the professor’s requirement.

#### ✔ 2. Evaluate both possible depth-2 trees

We manually compute total impurity for:

- A → B (greedy)  
- B → A (optimal candidate)

Results:

Greedy tree (A first): impurity = 0.1667  
Optimal tree (B first): impurity = 0.0000  

Thus:

- The B → A tree perfectly separates the data, while  
- the A → B tree contains an impure leaf, proving greedy is suboptimal.

---
### 3) ANIMATION — Three Unit Vectors with Equal Pairwise Correlation (from class discussion)

The animation in the "3 vector" python file illustrates how three unit vectors in 3D space behave when all pairwise correlations (dot products) are constrained to be equal and gradually vary from ρ = 1 down to the minimum possible value ρ = −1/2.

When the vectors satisfy
X·Y = X·Z = Y·Z = ρ,
their geometry is restricted by 3D space. In particular, ρ cannot be less than −1/2, because no three unit vectors in 3D can all have pairwise correlation lower than −1/2.

* At ρ = 1, all three vectors are perfectly aligned.

* At ρ = 0, they are roughly orthogonal.

* At ρ = −1/2, they achieve their maximum possible separation, forming 120° angles with each other.
