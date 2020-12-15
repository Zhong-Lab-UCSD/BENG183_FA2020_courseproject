# K-Means-Intros, Algorithms, and Limitations


K-Means Clustering: 
1. [Introduction](#1)
2. [Algorithm](#2)
3. [Implementations](#3)
4. [Limitations and Advantages](#4)

## 1. Introduction<a name="1"></a>
**K-means clustering** is a **clustering** algorithm that partitions n objects into **k** groups in which each object belongs to the cluster with the nearest **mean** (aka. cluster centroid). In bioinformatics, K-means can be used to find the genes that share common expression patterns across different samples and the patients that share similar gene expression patterns, etc. We will show an example of the second application in the following sections. Compared to other clustering methods, K-means clustering can work with large datasets in an efficient runtime.

## 2. Algorithm<a name="2"></a>
In a nutshell, K-means clustering begins with randomly selected centroids (graph b), assigns objects to the closest cluster (graph c), updates the centroids based on the current assignment of objects (graph d), and repeats the previous two steps (graph e and f) until it reaches convergence.
![Visualization of k-means algorithm](https://github.com/YingxuePan/Applied-Genomic-Technologies/blob/master/Group23Pics/kmeansalgo.png)

The pseudocode of K-means clustering is as follows:
```
kmeans(X: {x_1,x_2,...,x_n}, k)
	centroids: {c_1,c_2,...,c_k} = random_points(k)     \\randomly initialize k centroids
	Y: {y_1,y_2,...,y_n} = new list(n)                  \\initialize the output list
	while the clustering changes: 
		for x_i in X:
			y_i = closest_centroid(centroids,x_i)       \\find the closest centroid for each data point
		for c_i in centroids:
			c_i = update_centroid(Y)                    \\update each centroid based on current assginment
    return Y
```

## 3. Implementation<a name="3"></a>
With a given dataset, we could perform K-Means clustering easily through the steps below:
1. Normalizing the raw data
2. Choosing a statistically reasonable k: Elbow Method
3. Initializing Centroids
4. Code Implementation
5. Visualization (Plotting) of the Clustering Results

### 3.1. Normalizing the raw data
An important step we have to do before we actually use k means clustering to process our data is normalization. 

## 4. Limitations and Advantages<a name="4"></a>
1. Limitations of K-means Clustering
2. Advantages of K-means Clustering
### 4.1 Limitations of K-means Clustering