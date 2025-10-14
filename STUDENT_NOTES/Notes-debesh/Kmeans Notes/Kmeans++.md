# K–Means++

K–Means++ is an improved initialization method for K–Means that aims to select initial centroids in a way that increases the likelihood of converging to a good clustering.  

## Procedure
1. Choose the first centroid randomly from the dataset.  
2. For each remaining point, compute its **distance squared** to the nearest already chosen centroid.  
3. Select the next centroid randomly, with probability proportional to its squared distance.  
4. Repeat until *k* centroids are chosen, then proceed with standard K–Means iterations.  

---

## Example

Suppose we have 5 points:  
**$X = {1, 2, 4, 8, 9}$**  
We want to initialize **$k$ = 2**, using K–Means++.

1. Pick random centroid:  
   Let **$C₁ = 1$**
2. Compute distances squared to nearest centroid:

| Point | Distance to nearest centroid | Distance² |
|-------|-------------------------------|-----------|
| 2     | 2 – 1 = 1                     | 1         |
| 4     | 4 – 1 = 3                     | 9         |
| 8     | 8 – 1 = 7                     | 49        |
| 9     | 9 – 1 = 8                     | 64        |

3. Select next centroid with probability proportional to distance²:  

   Total distance² = **$1 + 9 + 49 + 64 = 123$**

| Point | Distance² | Probability |
|-------|-----------|-------------|
| 2     | 1         | 1/123 = 0.008 |
| 4     | 9         | 9/123 = 0.073 |
| 8     | 49        | 49/123 = 0.398 |
| 9     | 64        | 64/123 = 0.520 |

Based on these probabilities, **$9$ is picked randomly as $C₂$** (Black box method is used)

Proceed with K–Means using centroids **$C = {1, 9}$**.

---

# Black Box

The **black box** refers to the randomized selection step for picking new centroids.  

- After the first centroid is chosen randomly, each subsequent centroid is chosen using a probability distribution based on squared distances.  
- The exact point that gets picked is determined by a randomized procedure (the black box) that samples from this probability distribution.  
- In practice, this is done by generating a random number between 0 and 1 and mapping it onto the cumulative probability distribution (CDF) of the squared distances.  

Thus, the black box is the **Random Sampling Mechanism**:

- **Input:** list of probabilities proportional to squared distances.  
- **Output:** one data point chosen as the next centroid.  

---

## Continuing Example

After computing probabilities, we build the **Cumulative Distribution (CDF):**

| Point | Probability | Cumulative Probability |
|-------|-------------|-------------------------|
| 2     | 0.008       | 0.008                   |
| 4     | 0.073       | 0.008 + 0.073 = 0.081  |
| 8     | 0.398       | 0.081 + 0.398 = 0.479  |
| 9     | 0.520       | 0.479 + 0.520 = 0.999 (~1.0) |

### Using Black Box
1. Generate random number **$r ∈ [0, 1]$**.  
   Example: **$r = 0.72$**  
2. Find where r falls in the cumulative distribution.  
   Since **$0.72$ is between $0.479$ and $0.999**$, thus point **9** is chosen.  

---
