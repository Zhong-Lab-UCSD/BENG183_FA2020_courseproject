# *k*-means Clustering & Analysis
#### By Group 16 - Meggan Uyeda, James Medwid, Brian Kauffman

## Table of Contents
1.  [Overview of Clustering and *k*-means](#01)<br>
1.1. [Clustering](#011)<br>
1.2. [*k*-means Clustering](#012)<br>
1.3. [Pros & Cons](#013)

2. [Applications of *k*-means](#02)

3. [The Algorithm](#03)<br>
03.1. [*k*-means Algorithm](#031)<br>
03.2. [Data Interpretation](#032)

4. [Choosing a value of *k*](#04)<br>
4.1. [The Elbow Method](#041)<br>
4.2. [The Silhouette Method](#042)<br>
4.3. [Silhouette Plots](#043)

5. [Distance Measures](#05)<br>
5.1. [Common Distance Measures](#051)<br>
5.2. [Accuracy of Distance Measures](#052)<br>
5.3. [Runtime of Distance Measures](#053)

6. [Variations of *k*-means](#06)<br>
6.1. [Fuzzy *k/c*-means](#061)<br>
6.2. [Hybridized *k*-means](#062)

7. [Summary](#07)

8. [References](#08)


## 01 - Overview of Clustering and *k*-means<a name="01"></a>
### 01.1 - Clustering<a name="011"></a>
**Clustering** is an unsupervised, machine learning technique used to group data into multiple clusters to further be analyzed. Data that is grouped within the same cluster have more similar features when compared to the data grouped in with a different cluster. Some examples of clustering methods are *k*-means clustering, agglomerative hierarchical clustering, mean-shift clustering, and density-based spatial clustering of applications with noise (DBSCAN). Clustering can then be used to classify and label various subgroups of data.

### 01.2 - *k*-means Clustering<a name="012"></a>
***k*-means clustering** finds the similarity, or distances, amongst all the given data points based on an arbitrary centroid. In this iterative algorithm, *n* represents the number of data points, *k* represents the number of clusters, where 1 < *k* ≤ *n*, and the centroids represent the mean vector of each cluster.

<img src=images/overview.png title=https://towardsdatascience.com/k-means-a-complete-introduction-1702af9cd8c>

### 01.3 - Pros & Cons<a name="013"></a>

**Pros:**

*  The algorithm has good, linear time complexity of O(*n*) or, to be more specific, O(*tknd*) where *t* = # of iterations, *k* = # of clusters, *d* = # dimension of each object, *n* = # of objects, where *k,t,d << n*. 
* Hence, this gives us the ability to perform the algorithm on large data sets that would be much slower with other clustering methods.
* When clusters are distinct, well-separated, and/or show a spherical shape, the algorithm typically yields accurate results.

**Cons:**

* The algorithm may produce different results on multiple runs based on initial centroid selection. Hence, we need to make sure our centroid selection process is accurate before running the series of steps.
* Outliers can negatively affect the clusters, in which case they should be removed before performing the algorithm.
* To get the best results, an appropriate *k* must be specified. This means knowing the number of *k* in advance or calculating it via one of the methods [we will describe later](#04).

---
## 02 - Applications of *k*-means to Bioinformatics<a name="02"></a>
*k*-means clustering is a common technique used in various areas of research. It is often used to cluster data from gene expression levels, protein-protein interactions, and DNA sequences. By grouping together similar gene expression levels, the number of associated proteins within a protein network, and the sequences of various DNA, scientists can more easily identify the functionality of related genes, determine the structure of protein interaction networks and pathways, and distinguish the virulence of different DNA sequences, respectively.

---
## 03 - The Algorithm<a name="03"></a>
### 03.1 - *k*-Means Algorithm<a name="031"></a>
Given *k*,
1. Plot objects into arbitrary, *k* spaces.
2. Choose an arbitrary centroid for each cluster.
3. Tether each object to a respective cluster.
4. Calculate the difference between each point and its respective cluster.
5. Reallocate data points with a minimum distance to the centroid to be in a cluster.
6. Calculate the new centroid (mean) of each new cluster.
7. Repeat until the algorithm reaches convergences or the maximum number of iterations have been fulfilled.

In the figure below, we see the iterations of the *k*-means algorithm, where *k* = 3. The stars represent the centroids and the data points that belong to each cluster are color-coded to each respective cluster.
<img src=images/cluster_anim.gif title=Algorithm_[3]>


### 03.2 - Data Interpretation<a name="032"></a>

After clustering the data points, the clusters can be analyzed using one of the two approaches:
* **Empirical Approach**
1. Separate the data points that belong to each cluster into a separate list or matrix.
2. Identify each data points’ characteristics.
3. Study the differences amongst the clusters’ dimensions to distinguish the clusters.
4. Make a hypothetical guess on what each cluster represents.

For example, below we see on the x-axis, a feature of interest, while on the y-axis, we see the mean of that value.

<img src=images/ana_emp.png title=Empirical_[9]>

* **Centroid Approach**
1. Determine the data point closest to the centroid and label it the “representative” data point.
2. Using the representative data point, we can study the data point along its dimensions to distinguish the clusters’ profile.
3. Make a hypothetical guess on what each cluster represents using the representative data point.

For example, we can see a Centroid Approach below, where the representative data point is depicted by the red stars.

<img src=images/ana_cent.png title=Centroid_[9]>

In either approach, there must be assumptions made about the characteristics that determine each cluster. However, in the Centroid Approach, if the variance of the data points within the cluster is high, then the representative data point would not be a well-suited approach to distinguish the clusters.

---
## 04 - Choosing a value of k<a name="04"></a>
Ideally, we know the **value of** ***k*** we need up front. For example, if we’re trying to analyze differentially expressed genes between WT patients and patients with either of two oncogenic mutations, we would want to pick a value of 3 for *k* to fit the expression profiles to one of these 3 patient classifications.

However, for some datasets, *k* might not be given or immediately obvious to us. In this case, we have to further examine our data to **find the best value for k**. There are a few challenges involved with finding a *k* value. If we choose a *k* too small, we lose specificity by classifying points together that should be separate. Conversely, if we choose a *k* too large, we lose the information provided by the clusters, as they either become exceptionally small or single data points altogether. To prevent misinterpretation with our data, we have a few approaches to mathematically or visually determine the ideal value for *k*, namely the Elbow method and the Silhouette method.  

### 04.1 - The Elbow Method<a name="041"></a>

<img src=images/elbow.png title=Elbow_[12]>
The idea of the **elbow method** is to find the “elbow” of a graph of some scoring method against *k*. The elbow is the inflection point where we start seeing diminishing returns in increasing the value of *k*, or where the graph begins to level off. The elbow method typically seeks to minimize the overall distortion score (sum of squared distances between each centroid and the points assigned to it) of the plot, but may also use silhouette scores or other scoring functions.

### 04.2 - The Silhouette Method<a name="042"></a>
The idea of the **silhouette method** is to calculate the similarity of each point to the points in its cluster and its dissimilarity from the points in other clusters.

**Calculating similarity, *a*:**

<img src=images/form_sila.jpeg title=Similarity_[5]>


**Calculating dissimilarity, *b*:**

<img src=images/form_silb.jpeg title=Dissimilarity_[5]>


**The final score,** ***s*** (if there is only one point in the cluster, the score is always 0):

<img src=images/form_sil.jpeg title=Silhouette_Formula_[5]> 


Following this formula, we will get a **silhouette score** that is between -1 and +1. A score close to +1 tells us that the point is well-categorized—it is similar to the other points in its cluster, while being distant from points in other clusters. A score closer to 0 tells us there is more ambiguity—the point is roughly on the border between clusters. Finally, a negative score tells us that the point has probably been misplaced—it is more similar to points in one or more other clusters than it is to the points in its own. This may happen if the initial centroid selection was off, causing the algorithm to miscategorize some points, or if the clusters have irregular, non-spherical shapes. 

Once we have calculated the score for all points, we can compute the **average silhouette score** for this value of *k*. Good clustering will usually result in the highest average silhouette score. We could use this in the elbow method as described above (note that for silhouette scores we’d want to find a maximum rather than a minimum), or we could take a more visually intensive approach by creating **silhouette plots** to confirm our numeric findings.

### 04.3 - Silhouette Plots<a name="043"></a>
**Silhouette plots** graph the sorted silhouette scores of each cluster, allowing us to see if any plots have unusually high or low average scores as well as the relative size of each cluster. Here’s an example of two silhouette plots showing **bad clustering**, with the silhouette plot on the left and the color-coded scatter plot on the right:

<img src=images/sil_3.png title=Bad_Clustering_k3_[5]>

<img src=images/sil_5.png title=Bad_Clustering_k5_[5]>

In both of the silhouette plots on the left, we can see a significant issue with one or more clusters: every point in them is below the red line denoting the average silhouette score. This means that these clusters are poorly formed—either they have too many points to maintain internal similarity and have to be split, as is the case for the *k* = 3 example, or they are creating dissimilarity between each other by competing for the space of what should be a single cluster, as in the *k* = 5 example.

Here’s two examples of much better cluster formation on the same data:

<img src=images/sil_2.png title=Good_Clustering_k2_[5]>

<img src=images/sil_4.png title=Good_Clustering_k4_[5]> 

In both of these examples, each cluster has some points above the mean silhouette score. We could think of these as “core” components of each cluster—the ones that make it significantly distinct from those near it. The other points in the cluster are then classified with slightly less confidence. The presence of these core elements in every cluster (and that the average silhouette score remains high) indicates that we have **good clustering** for these values of *k*. 

We may also notice that the mean silhouette score for *k* = 2 is higher than that for *k* = 4—a value of 0.70 vs one of 0.65. But which is a better fit for the data? Looking at the plots on the right, we can see two different ways to categorize the clusters. For *k* = 2, we see one large cluster made up of 3 sub-clusters, while for *k* = 4 these sub-clusters are separate. If the distinction between these sub-clusters is important—for example, if the single cluster is a WT patient and the sub-clusters are different subtypes of a cancer—the classification could be important in determining our conclusions. But, if our goal is merely to tell whether a patient is healthy or not, we would get by just as well with the *k* = 2 version of the plot. This is why the silhouette method is valuable—it allows us to make analyses of the benefits of different *k* values beyond a simple score. 

---
## 05 - Distance Measures<a name="05"></a>
### 05.1 - Common Distance Measures<a name="051"></a>
**Manhattan, Euclidean, Cosine**, and **Correlation**.

All distance measures take two points (*a,b*) or (*x,y*) and perform some operation scaling on the number of dimensions in the space, *i*.

The Manhattan distance is the measurement between two data points along the axes at right angles, defined by:
<img src=images/form_man.png width=425 title=https://dev.to/trossii/k-nearest-neighbors-using-what-is-around-you-to-make-a-prediction-514j>

The Euclidean distance is the length of a straight line that connects two points, defined by:
<img src=images/form_euc.png width=425 title=https://aigents.co/blog/publication/distance-metrics-for-machine-learning>

The Cosine distance is the measurement of the angle between two non-zero vectors, defined by:
<img src=images/form_cos.png title=https://www.machinelearningplus.com/nlp/cosine-similarity/>

The Correlation distance is the measurement of dependence between two paired, random vectors, defined by:
<img src=images/form_corr.png title=https://towardsdatascience.com/log-book-guide-to-distance-measuring-approaches-for-k-means-clustering-f137807e8e21>

### 05.2 - Accuracy of Distance Measures<a name="052"></a>
Existing literature suggests that clusters formed using correlation coefficients as the distance measure produced clusters with the most ideal silhouette scores. In these plots for a 4-dimensional, 150-sample dataset, Euclidean-based clustering significantly miscategorized several points that were more correctly placed with Correlation distance. However, it remains important to test which method generates the best clustering for your own data if given the option. 

<img src=images/sil_euc.png width=400 title=Euclidean> <img src=images/sil_corr.png width=400 title=Correlation_[4]>



### 05.3 - Runtime of Distance Measures<a name="053"></a>
In this same study, Manhattan distance yielded the best runtime, while Cosine distance ran the slowest. Although some calculations are more computationally intensive than others, it’s worth bearing in mind that these more complex distance measures may be capable of yielding a faster termination if they reduce the number of iterations needed to reach optimal clustering. Hence, if possible, it’s good to test which method runs quickest for the size and type of data you will be analyzing. 

<img src=images/runtime_s.png width=425 title=4-dimensional_[4]> <img src=images/runtime_l.png width=425 title=13-dimensiona_[4]l> 

---
## 06 - Variations of *k*-means<a name="06"></a>
While the original *k*-means algorithm has some limitations, there are some additional variations of the algorithm that may help overcome these limitations. These variations allow *k*-means to be used for more complex tasks, for more diverse sets of data, and to enable its continued development for future needs. 

### 06.1 - Fuzzy *k/c*-means<a name="061"></a>
* Each point is assigned a weight for each cluster, dictating **how strongly** it belongs to that particular cluster rather than explicitly assigning a category to the point.
* This is useful for applications where data points may belong to more than one distinct set—for example, if we want to determine whether a group of patients has one *or more* genetic disorders rather than which single one they have. 
* In bioinformatics, this has been used to identify biologically-related genes from microarray data with better accuracy than non-fuzzy clustering.  

### 06.2 - Hybridized *k*-means<a name="062"></a>
* Fuses additional algorithms onto *k*-means clustering.
* For example, the Incremental Genetic *k*-means Algorithm applies genetic operators to the population prior to each iteration of *k*-means.
	* Selection chooses representative samples with good fitness values to move on to the next step of the algorithm.
	* Mutation randomly modifies these selected samples to maintain diversity in the dataset. 
<img src=images/gen_algo_approach.png title=IGKA_[11]>

* These algorithms also typically implement more advanced initial centroid selection methods to decrease the number of iterations the algorithm has to go through and to improve the final results. 
* In general, these algorithms are useful for high-dimensional data and are particularly specialized to the task they’re attempting to solve.

---
## 07 - Summary<a name="07"></a>
In conclusion, *k*-means clustering is a powerful machine learning tool used to cluster data points into smaller subgroups that can later be analyzed and classified. Using this approach, we can identify protein structures, compare DNA sequences, and analyze gene expression. This is important in order to better understand complex processes in the age of medicine and biotechnology. More specifically, *k*-means clustering can be fine-tuned to meet the needs of diverse and large data sets, such as choosing an optimal *k*-value, using different distance measures, and selecting a variation of the *k*-means algorithm. Further, we can gather timely and accurate data using the correct distance measure and algorithm variations.

---
## 08 - References<a name="08"></a>
1. [*k*-means Cluster Analysis · UC Business Analytics R Programming Guide. ](https://uc-r.github.io/kmeans_clustering#kmeans)
2. [How to Determine the Optimal *k* for *k*-Means? | by Khyati Mahendru | Analytics Vidhya | Medium. ](https://medium.com/analytics-vidhya/how-to-determine-the-optimal-*k*-for-*k*-means-708505d204eb)
3. [*k*-Means Clustering Algorithm.](https://medium.com/@imparth/*k*-means-clustering-algorithm-34807a7cec71)
4. [Bora, Dibya & Gupta, Dr. (2014). Effect of Different Distance Measures on the Performance of *k*-Means Algorithm: An Experimental Study in Matlab.  ](https://arxiv.org/ftp/arxiv/papers/1405/1405.7471.pdf#:~:text=In%20K%2DMeans%20algorithm%2C%20we,role%20in%20the%20clustering%20algorithm)
5. [Scikit-learn: Machine Learning in Python, Pedregosa et al., JMLR 12, pp. 2825-2830, 2011. ](https://scikit-learn.org/stable/auto_examples/cluster/plot_kmeans_silhouette_analysis.html)
6. [Limin Fu and Enzo Medico, BMC Bioinformatics Clusters from fuzzy memberships analyzing DNA microarray data. ](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-8-3/figures/1)
7. [ AIP Conference Proceedings 1862, 030134 (2017); Published Online: 10 July 2017. ](https://doi.org/10.1063/1.4991238)
8. [Lin C, et al. Xiaohua H,  Pan Y. Clustering methods in protein-protein interaction network, Knowledge Discovery in Bioinformatics: Techniques, Methods and Application, 2006John Wiley & Sons, Inc.](https://cse.buffalo.edu/DBGROUP/bioinformatics/papers/chuan.pdf)
9. [“So You Have Some Clusters, Now What?” Square Corner Blog, 9 Nov. 2017. ](developer.squareup.com/blog/so-you-have-some-clusters-now-what/) 
10. [Oyelade, Jelili et al. “Clustering Algorithms: Their Application to Gene Expression Data.” Bioinformatics and biology insights vol. 10 237-253. 30 Nov. 2016, doi:10.4137/BBI.S38316](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5135122/)
11. [Dembélé D, Kastner P. Fuzzy C-means method for clustering microarray data. Bioinformatics. 2003 May 22;19(8):973-80. doi: 10.1093/bioinformatics/btg119. PMID: 12761060.](https://pubmed.ncbi.nlm.nih.gov/12761060/) 
12. [“Elbow Method” Elbow Method - Yellowbrick v1.2 Documentation](www.scikit-yb.org/en/latest/api/cluster/elbow.html)


---

