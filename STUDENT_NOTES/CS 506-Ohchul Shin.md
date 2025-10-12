9/10  
equation: diff of x \+ diff of y / sqrt(diff of x ^ 2 \+ diff of y ^ 2\)  
Correlation: close to 1: likely to form a linear relation.  
Close to 0\. Some even spread around the axis. 

9/15  
Data: rows of distinct data points, columns of features.   
Feature space: 2D Euclidian plane that data points can exist.

How close are the data?  
Dissimilarity: returns a large value for points far away. 

- Distance function  
  if and only if property: d(i, j) \= 0 if and only if they are equal

     		d(i,j) \= d(j, i)  
     		d(i,j) \= d(i,k) \+ d(k,j)     
- Minkowski distance:

		p is a parameter that defines the function.   
		equation: Lp \[sum of {(x \- y) ^ p }\] ^ 1/p   
		When p \= 2, Euclidian distance: Unique shortest path  
		When p \= 1, Manhattan distance: Multiple shortest paths

- Jaccard Similarity

		Number of intersection / number of union

- Cosine similarity

  s(x,y) \= cos(theta)

Clustering  
	Arbitrary, can be Ambiguous

- Partitional  
  	Goal: Partition dataset into k partitions. Input: K  
  	How many clusters should be made?   
  	Create clusters with smaller variance.   
  		Algorithm?  
  		cost function: minimize K means  
  		Lloyd’s algorithm:   
  			Randomly pick k centers.   
  			Assign points to nearest center  
  			Compute the new centers as the means of each cluster.   
  		Guaranteed to converge

    
  Depends on the starting point.  
  solution: farthest first traversal. (can not deal with outliers)  
  The probability of picking next point is proportional to the distance.   
  Cons: Does not deal with elongated clusters. 


Silhouette score  
ai: smallest mean distance from a point to every other point within its cluster  
bi: smallest mean distance from a point to every other point in another cluster 

- Hierarchical  
  	At every step, merge clusters to produce a dendrogram   
  	Cut at threshold to produce any number of clusters  
  	Agglomerative method

  Start every point in its own cluster  
  At each step, merge two closest clusters  
  Stop when every point is in the same cluster	  
    
  Single-link distance: minimum of all pairwise distance within points in different clusters  
  Complete link: Max d  
  Average link:   
  Ward’s distance: Var within merged cluster \- Var of cluster 1 \- Var of cluster 2

  Divisive method  
  Start with every point in same cluster  
  split every point is in own cluster  
  	  
- Density \- Based

  Look for regions with high density

  Density? Grow a circle with radius r, and fit certain amount of points


- Soft Clustering (Probabilistic)

		k clusters, assign data with k probabilities to belong in each cluster.  
		EM algorithm

Clustering Aggregation  
	terminology: clustering output: output of clustering algorithm  
	  
Comparing clusters: Pick random points and check whether they belong to same   
cluster

- Disagreement distance: Sum of Indicator function (return 1 when disagree, 0 otherwise)

Aggregate clustering: clustering categorical data

SVD(Singular value decomposition)   
\- Reduce dimension of data / feature selection  
\- Data approximation  
\- Anomaly detection & Denoising

A (n,m matrix)= UV (U \= n,k)(V \= k,m)  
SVD \= UEV^T  
E \= {only diagonal entries, strictly decreasing values as rank increase}  
Frobenius distance: Euclidian distance for matrix. Pairwise distance for components of matrix

ith singular vector represents ith most variance

