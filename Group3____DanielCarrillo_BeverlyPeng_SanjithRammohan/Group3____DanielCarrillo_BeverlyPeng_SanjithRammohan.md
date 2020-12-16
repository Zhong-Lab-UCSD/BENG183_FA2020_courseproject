# Hierarchical Clustering

## Table of Contents
1. General Overview

2. Inputs, Outputs, and Variations

3. Algorithm

4. Algorithm Approaches

5. Similarity measure

6. Linkage Methods

7. Applications


## 1. General Overview

There are many strategies to cluster data, all of which depend on what the ultimate goal is. Clustering is an **unsupervised** learning problem, meaning the algorithm does not have a reference to check accuracy. All of them rely on different mathematical computations that are used to determine how similar these data are. When these similarities are weighted differently, various clustering patterns can occur. 

**Hierarchical clustering** is one of these methods where the goal is to input a data matrix and output a clustering of groupings that represent similarly expressed data closer within clusters than across other clusters. 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/11andtwoforyoubecausedanthoughtheshouldredo.png" width = 1000>

## 2. Inputs, Outputs, and Variations

**Input**: As mentioned above, typically the input for clustering is given as a distance matrix or set of vectors that represent the expression value or variance amongst the data points.

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/3.png" width = 200>

**Output**: The result of clustering should produce a visual representation of the cluster groups which display the closely related data points at shorter distances compared to other data points at larger distances amongst the given set.

**Scatter Plot**: Displays collection of data through a correlation relationship and distance between points representing similarity. Clusters are usually marked by color or dividing lines

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/4.png" width = 400>

**Venn Diagram**: Also displays hierarchical clustering illustrating similarity with overlapping points in same plane however similarity is not quantitatively represented

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/5.png" width = 300>

**Dendrogram**: A diagram that represents a tree that shows the relationship of the similarity between the input data’s clusters. It usually takes the form of a binary tree where each smaller subset of the data considered compares more specific traits to the identity of the smaller subset. 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/6.png" width = 300>

#### Variations: 

**Agglomerative**: (bottom up) start with n single clusters and merge the most similar clusters together forming hierarchy, and keep continuing

**Decisive**: (top down) start with all samples in one cluster and then start splitting up clusters by determining the most contrasting points to form hierarchy

## 3. Algorithm

Agglomerative Hierarchical Clustering Steps:
1. Assign all the points to an individual cluster
2. Merge the points with the smallest distance
3. Repeat step 2 until only a single cluster is left

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/7.png" width = 400>

Decisive Hierarchical Clustering Steps:
1. Assign all the points to one cluster
2. Divide the points into two different clusters based upon the largest distance difference
3. Repeat step 2 until only single points are left

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/8.png" width = 400>

## 4. Algorithm Approaches

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/9.png" width = 350>

The goal of hierarchical clustering is simple: to build a tree diagram where the input data that are most similar to each other are placed on branches that are closer together, called a dendrogram. We know how close branches are to one another based on the height of the branch, which represents the amount of dissimilarity between clusters (see image above). The further to the right that the dendrogram the branch splits, the larger the dissimilarity value, meaning the more different the clusters are from one another. Walking through the algorithm step to step, it soon becomes clear that the features that merge into the same cluster sooner are more similar than those that merge later.

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/10.png" width = 600>

If one approaches the hierarchical clustering algorithm more vigorously, it soon becomes clear that the distance between the clusters is simply the difference between the chosen similarity metric the data is being evaluated with (which is discussed more in the next section) thus making hierarchical clustering an excellent tool when visualizing the similarities and differences between the data.

## 5. Similarity Measure

Similarity between the new clusters formed and all remaining clusters can be calculated with various clustering methods:

**Euclidean Distance**: 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/EuclideanDistance.PNG" width = 250>

- Most common method 
- Measures similarity by calculating distance between two points
- Runtime: O(n)
- Advantages: easy to compute, works well with compact  datasets
- Disadvantages: sensitive to outliers


<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/Euclidean.png" width = 250>

**Manhattan Distance**: 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/ManhattanDistance.PNG" width = 250>

- Typically used when there is high dimensionality and a grid like pattern of data
- Ex. when calculating distance on a game board or map 
- Runtime: O(3n)
- Advantages: used to detect outliers, or higher planes
- Disadvantages: expensive in terms of computation

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/12.png" width = 250>

**Cosine Distance**: 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/CosineDistance.PNG" width = 200>

- Preferred in collaborative filtering, finding similarity between vectors  
- Ex. user similarity amongst apps such as movie/music recommendation for similar parties/clusters 
- Runtime: O(3n)
- Advantages: independent of vector length, unaffected by rotation
- Disadvantages: affected by linear transformations

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/13.png" width = 250>

## 6. Linkage Methods

There are several methods to determine which points in each cluster the similarity measure will be calculated with: 
- Centroid
- Single Linkage
- Complete Linkage
- Average Linkage
- Ward’s Method

Having a clear understanding of what your data looks like visually and what clusters you expect are important when choosing which linkage method to use. 


**Centroid method**: utilizes a centroid to group clusterings. A **centroid** is a point that represents the mean value of all the points in the cluster. Once the subclusters are merged, a new centroid must be calculated for the following iteration.

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/14.png" width = 250>

**Single linkage**: minimizes the dissimilarity between the two closest points belonging to two different clusters. The two clusters with the lowest dissimilarity  will be merged and the next iteration occurs. 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/15.png" width = 250>

**Complete linkage**: is the same as single linkage except the two farther points’ dissimilarity value is used. 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/16.png" width = 250>

**Average linkage**: calculates the average dissimilarity  between all the points in one cluster and all the points in another cluster. The two clusters with the lowest dissimilarity  average will be merged. 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/17.png" width = 250>

**Ward’s method**: is an agglomerative approach to hierarchical clustering. Rather than using the dissimilarity metric, Ward’s method looks at the variance of possible cluster merging pairs and merges the clusters with the lowest variance. 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/Wards.png" width = 450>

## 7. Applications

Hierarchical clustering has many gene expression related applications. Dendrograms are very important in visualizing the similarities and differences between clusters. Below is an example of a complete linkage hierarchical clustering method by Chen et al. [9] used to create a dendrogram showing the relationship between gene expression patterns of various human and mouse brain tissue samples. 

<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/18_allex.png" width = 800>

As panel a above shows, analogous tissues across species were clustered together as opposed to species clustering together at the most granular level. This method of clustering can be compared with the PCA shown in panel b. Hierarchical clustering appears to perform better with the expected tissue and species results. 

There are also many non-gene expression applications of hierarchical clustering. This method can also be applied to analyzing the online relations between political senators and party affiliation [10]. Looking at the left panel below, it can seem like a daunting task trying to find the relations between the red (Republican), blue (Democratic), and black (independent) senators. 


<img src="../Group3____DanielCarrillo_BeverlyPeng_SanjithRammohan/19_allex.png" width = 800>

After applying hierarchical clustering of the Twitter followings of various U.S. senators, there is a clear split in the clustering pattern between Republicans and Democrats. By taking a deeper look into the meaning behind each branch split, additional political beliefs may be inferred as well. 

## References

1. https://www.data-to-viz.com/graph/dendrogram.html
2. https://www.sciencedirect.com/topics/computer-science/hierarchical-cluster-analysis 
3. https://www.displayr.com/what-is-hierarchical-clustering/ 
4. https://stackoverflow.com/questions/52876680/clustered-scatterplot-in-r
5. https://www.i2tutorials.com/what-is-the-difference-between-euclidean-manhattan-and-hamming-distances/
6. https://www.geeksforgeeks.org/ml-hierarchical-clustering-agglomerative-and-divisive-clustering/ 
7. https://www.researchgate.net/figure/Dendrogram-and-Venn-diagram-representation-of-Agglomerative-Hierarchical-Clustering_fig3_221324943
8. https://towardsdatascience.com/hierarchical-clustering-and-its-applications-41c1ad4441a6
9. https://doi.org/10.1371/journal.pone.0164295
10. https://towardsdatascience.com/hierarchical-clustering-and-its-applications-41c1ad4441a6

