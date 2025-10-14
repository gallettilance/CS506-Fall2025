# Exploring the Right k in Clustering

Choosing the appropriate number of clusters (**$k$**) is critical for meaningful clustering results. Several methods and metrics help in deciding the optimal $k$.  

In the ipynb and PDF I have plotted elbow, silhouette scores and Gap stats for different datasets, do have a look!

---

## Methods to Choose $k$

### 1. Elbow Method
- Plot the **within-cluster sum of squares (WCSS)** against different values of $k$.  
- Look for an **“elbow” point** where adding more clusters does not significantly reduce WCSS.  

### 2. Silhouette Score
- Measures how similar a point is to its own cluster compared to other clusters.  
- Range: **-1 to 1**
  - 1 → well-clustered  
  - 0 → on the boundary  
  - Negative → misclassified  
- Compute the **average silhouette score** for different k values.  
- Choose $k$ that **maximizes the score**.  

### 3. Gap Statistic
- Compares WCSS of your clustering with WCSS of randomly distributed points.  
- The optimal $k$ **maximizes the gap** between your clustering and random clustering.  

### 4. Domain Knowledge
- Sometimes the best $k$ is informed by the **specific application or business problem** rather than pure statistics.  

---

## Gap Statistic Explained

The Gap Statistic helps choose the optimal number of clusters by comparing your clustering result to random data.  

- If your clustering is meaningful, the **within-cluster dispersion** should be smaller than what you’d get with random points.  
- It measures how much better your clusters are than random noise.  

### Understanding with an Example

Imagine sorting **candies into jars**:

- We have a bunch of candies, which represent our data points.
- We want to put them into k jars (clusters) so that similar candies go together.
- After putting candies in jars, we check: “How close are the candies in each jar?”
- If candies are close → jar is neat → small WCSS.
- If candies are spread out → messy → big WCSS.
- Now, imagine if candies were thrown randomly on the table.
- Even if we try to put them in k jars, the jars won’t be neat.
- Measure the messiness (WCSS) of these random jars.
- Gap = “messiness of random jars” − “messiness of your actual jars”
- Big gap → our clustering is much better than random
- Small gap → our clustering is not much better than random

---

### Steps to Compute Gap Statistic

1. **_Compute WCSS for your data_**: “within-cluster sum of squares” (sum of squared distances from points to their cluster centroids).

2. **_Generate reference datasets_**: These are random points with the same shape as your data (same number of points and dimensions), usually uniformly distributed in the bounding box of your original data.

3. **_Cluster the reference datasets_**: For each k, compute WCSS for the reference datasets.

4. **_Compute Gap_**: $Gap(k) = \frac{1}{B} \sum_{b=1}^{B}( \log(W^*_{kb}) - \log(W_k))$
    
    Where:  
   - $(W_k)$ = WCSS for real data with k clusters  
   - $(W^*_{kb})$ = WCSS for b-th reference dataset with k clusters  
   - $B$ = number of reference datasets  
   - $( \log(W^*_{kb}) - \log(W_k))$ : Larger gap means our clusters are much better than random.

5. **Choose k** with maximum Gap.

> Unlike the Elbow Method, Gap adds a baseline for comparison. It asks:  *“Is my clustering actually meaningful, or would random points look just as good?”*  

---

## Evaluation Metrics for Clustering

1. **Centroid Distance**  
   - Distance between cluster centers.  
   - Goal: Larger → clusters are well-separated.  

2. **Silhouette Score**  
   - Measures closeness of each point to its own cluster vs nearest other cluster.  
   - Range: -1 to 1  
   - Goal: Higher → points well-clustered  

3. **Davies-Bouldin Index (DBI)**  
   - Ratio of cluster spread to distance between clusters.  
   - Goal: Lower → clusters tight and far apart  

4. **Between-Cluster Sum of Squares (BCSS)**  
   - Sum of squared distances from cluster centroids to overall mean.  
   - Goal: Higher → clusters are spread out  

5. **Within-Cluster Sum of Squares (WCSS)**  
   - Sum of squared distances of points to their own cluster centroid.  
   - Goal: Lower → clusters are cohesive  

6. **Gap Statistic**  
   - Compares WCSS of real data to WCSS of random points.  
   - Goal: Larger → clusters much better than random → optimal k  

---


