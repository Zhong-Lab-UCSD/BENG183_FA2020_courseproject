# KNN Algorithm
#### BENG183 Group 22 
#### Yingxi Lin, Shanqing Wang, Weiheng Zhang

## What is KNN?
KNN stands for K-nearest neighbors, where K is an integer value. It is one of the most basic supervised machine learning algorithms which relies on the concept that similar data tend to be located near each other. In principle, it can be used for both classification and regression problems, but in practice, it is more often used for classification. 
![](https://static.wixstatic.com/media/a27d24_ccd4139ebb364c7aa9e0723b4039b0f5~mv2.png/v1/fill/w_600,h_245,al_c/a27d24_ccd4139ebb364c7aa9e0723b4039b0f5~mv2.png)

The algorithm makes predictions based on similarities determined from the features of your sample set. In the image below, we are trying to classify foodstuffs into one class out of vegetables, fruits or proteins, based on the sweetness and the crunchiness of the food. In the case of a tomato, we would compare its sweet and crunchy level with other food in the training set and determine which class it belongs to.

![](https://2.bp.blogspot.com/-BNquM6A-d00/V8FfXbo8l2I/AAAAAAAAFPE/vXpXO7B4DxgU0-AltBc2y5IkVqRAuNNrQCLcB/s1600/ml7.png)

## How does the algorithm work?
Let's talk more in depth about how this algorithm actually works. First, we would need to have some training data. Because this is a supervised algorithm, the data needs to be already labeled. In this example, the green triangles and red stars are our training data set because it is labeled, and the question mark is the unknown data point that we want to classify.

![](https://i.imgur.com/y1fft6u.png)

To predict a new unlabled data point d, we would calculate the distances between d and each point in the training set. Next we will rank these distances from the shortest to the longest and select the top k number of nearest neighbors to vote on the prediction of the new data point d. Although it is not shown in the image below, we would calculate the distance between the question mark to all the red stars and green triangles to make sure we have the absolute closest points.

![](https://i.imgur.com/G1LVeJd.png)

For a regression problem, we would output the average of the neighbors's labels and for classification, the mode. In both of these cases, it can essentially be thought of as a majority voting situation. In the figure below, we set k to be 3 and we have two green and one red neighbors, so we would classify the new data point as a green triangle, or Class B.

![](https://i.imgur.com/CBGjSsz.png)


## How to fine tune the model?
This is an important question, as the choice of k greatly influences the accuracy of the model. If it is too small, the label given will be affected by outliers and noise in the data. If k is too large, not only will accuracy be hit, you also move farther away from the identity of looking at the close neighbors, which KNN should do. In the figure below, we see that a low k value of 3 can causes the blue dot to be possibly mislabeled as red when it should in fact be blue, as it would be labelled when k is 5.

![](https://cdn.analyticsvidhya.com/wp-content/uploads/2018/03/knn3-768x694.png)

A common practice for choosing k is to choose an odd value close to the square root of the total number of training samples. The odd-ness serves to remove the case of ties in binary classification scenarios, while the value itself functions decently as a go-to value in terms of accuracy. However, in order to optimize the accuracy of one model, people often perform cross-validation on a range of k-values to find the best one to use. This is often done with metrics such as accuracy, precision, recal, or f-score, just to name a few. One might generate a graph like the one below for different values of k, then choose the optimal k from the analysis. In this one scenario, a k of 10 or 11 is probably the best choice. 

![](https://www.analyticsvidhya.com/wp-content/uploads/2014/10/training-error_11.png)

Below is another way to visualize the effects of k-value choice on some training data. You can see that as k increases the decision boundary becomes smoother, indicating that the model will have better perfomance on test or unknown data. 

![](https://www.analyticsvidhya.com/wp-content/uploads/2014/10/K-judgement.png)
![](https://www.analyticsvidhya.com/wp-content/uploads/2014/10/K-judgement2.png)


## Prerequisites of KNN
We cannot use KNN on whatever data we get. There are certain prerequisites the dataset must fulfill to make sure that KNN will run correctly.

Firstly, we need to make sure all samples are correctly labelled. For the KNN question in our midterm 2 exam, if all healthy patients are mislabeled as having cancer AB, then our calculation will be ruined. For samples missing or having an incorrect label, we should either fix or discard them. 

Secondly, we need to make sure our dataset is clean. We should try to get rid of noise and outliers in the dataset. If we are trying to predict male and female from height and weight, samples labelled as “bio major” should not exist. We need to discard samples with extreme values because KNN is very sensitive to outliers and will produce inaccurate classification. Thus, for the samples with red colored labels and numbers in the following chart, we should either fix their value or discard them. 

![](http://i1.fuimg.com/572075/71b1e146bb9a1700.png)

We also need to make sure our dataset is balanced, which means the dataset should contain similar amount of “male” and “female” samples in this case. The chart on the bottom left shows an example of imbalanced data. We need to make our dataset looks like the chart on the right, because data imbalance will negatively impact KNN's classification accuracy.
![](http://i2.tiimg.com/572075/30cd51451c1b5e56.png)


Lastly, the dataset cannot contain too many samples, and each sample cannot have too many features. Because KNN is a lazy learning  algorithm (e.g., instance-based learning) without a training step, as it does not produce a discriminative function on the training data. This means the initial training step simply stores the training data, and computation doesn't happen until prediction time. This differs from eager learning, where a classification/regression model is constructed based on training data before prediction. In other words, KNN takes very little time in training, but much more time in predicting. If the training dataset contains too many samples, calculating distances between query point and the whole dataset would be very computational heavy. 

High dimensionality in the dataset not only make the computation heavy, but also will also decrease the accuracy of KNN. The figures below demonstrate "the curse of dimensionality". These figures plot the distribution of pairwise distances between randomly distributed points with different dimensions. As the dimensionality increase, the distances all clustered within a small range, which render the KNN model useless. 
![](https://www.cs.cornell.edu/courses/cs4780/2018fa/lectures/images/c2/cursefigure.png)


## Advantages and Disadvanage of KNN

### Pros
* KNN is very easy to learn. You can code your own from scratch in almost any programming language. The code snippet below is an example implementation of KNN based on Euclidean distance *(Brownlee)*.
```python    
# calculate the Euclidean distance between two vectors
def euclidean_distance(row1, row2):
	distance = 0.0
	for i in range(len(row1)-1):
		distance += (row1[i] - row2[i])**2
	return sqrt(distance)
 
# Locate the most similar neighbors
def get_neighbors(train, test_row, num_neighbors):
	distances = list()
	for train_row in train:
		dist = euclidean_distance(test_row, train_row)
		distances.append((train_row, dist))
	distances.sort(key=lambda tup: tup[1])
	neighbors = list()
	for i in range(num_neighbors):
		neighbors.append(distances[i][0])
	return neighbors
 
# Make a classification prediction with neighbors
def predict_classification(train, test_row, num_neighbors):
	neighbors = get_neighbors(train, test_row, num_neighbors)
	output_values = [row[-1] for row in neighbors]
	prediction = max(set(output_values), key=output_values.count)
	return prediction
```
* Does not require training step at all. Directly use the given dataset for prediction.
* Ease of application makes it very easy to be implemented on new problems. 
* Because KNN can do both classification and regression, it is powerful on a wide range of use cases. 
![](https://www.jeremyjordan.me/content/images/2017/06/Screen-Shot-2017-06-17-at-9.30.39-AM-1.png)

### Cons
* Lazy algorithm. Does not produce a discriminative function. Prediction speed is slower than other non-lazy algorithms. 
* Big dataset or samples with too many features greatly impact KNN's performance. High dimensionality of samples also decreases classification accuracy. 
* Sensitive to unclean dataset. Require a pre-check on the dataset to get rid of noise, outliers and data imbalance. 
* Users need to know how to choose a good k. A bad k value will ruin the accuracy. 

## Workflow
Let's walk through an example use case of KNN. Say that you were tasked to find a method to diagnose people as having Non-small Cell Lung Cancers (NSCLC) or not. One aspect of your approach could be to give a categorization based on the levels of expression from choice differentially expressed genes through KNN. You would begin by choosing the genes of interest, then gathering the label and gene expression data from a previous study, such as one shown below (Huang, 2018).

![](https://www.researchgate.net/publication/323499416/figure/fig1/AS:599537135648770@1519952200605/Heat-map-of-the-top-100-differentially-expressed-genes-including-50-up-and-downregulated.png)

You would make sure your data has been normalized, to remove any intrinstic biases that might be present. Below is an illustration of data before and after normalization. Notice that the x<sub>1</sub> has less of an impact on the NN classification before when compared to after.

![](https://i.stack.imgur.com/OCUmI.png)
![](https://imgs.developpaper.com/imgs/J5r01.png)

You would then split, some percentage of the data into training and save the remaining into a testing set for later verification. Your gathered data might look something like this.

![](https://puu.sh/GXWG6/b5b97b0aa5.png)

![](https://puu.sh/GVUEm/0222700f19.png)

Next, you would determine the best distance metric for your model. Common distance metrics used are Euclidean for Quantitative data and hamming for Qualitative. In the application of gene expression, Spearman and Pearson distance metrics have been used, one of which we would probably use for this case.

You would then run KNN on the previously set aside testing set to evaluate the effectiveness of your model, and decide if your model needs further tuning. Suboptimal levels of any of your testing values across all k-values may prompt you to reevaluate your training data or whole approach.

Finally, you would run your fully-developed KNN on new patient gene expression data to diagnose their condition. 

![](https://puu.sh/GXWEK/753beb59ff.png)
)

Because of your finely-tuned model, you should be confident that the labels are accurate, and therefore provide useful information to complete your task.

![](https://puu.sh/GXWCg/190200b1bd.png)







## Example use case
KNN has been used in different bioinformatics application:
- Mining high-dimensional microarray gene expression data (*Li et.al.*)
- Predicting membrane protein type (*Shen et.al*)
- Estimating missing data from DNA microarray (*Troyanskaya et.al.*)
## Refererences
- Hastie, Trevor. (2001). The elements of statistical learning : data mining, inference, and prediction : with 200 full-color illustrations. Tibshirani, Robert., Friedman, J. H. (Jerome H.). New York: Springer.

- Huang, Ru & Gao, Lei. (2018). Identification of potential diagnostic and prognostic biomarkers in non-small cell lung cancer based on microarray data. Oncology Letters. 15. 10.3892/ol.2018.8153. 

- N. S. Altman (1992) An Introduction to Kernel and Nearest-Neighbor Nonparametric Regression, The American Statistician, 46:3, 175-185, DOI: 10.1080/00031305.1992.10475879

- Simplilearn. KNN Algorithm Using Python | How KNN Algorithm Works | Data Science For Beginners | Simplilearn. YouTube, 6 June 2018, www.youtube.com/watch?v=4HKqjENq9OU.

- Srivastava, T. (2020, October 18). K Nearest Neighbor: KNN Algorithm: KNN in Python & R. Retrieved from https://www.analyticsvidhya.com/blog/2018/03/introduction-k-neighbours-algorithm-clustering/

- Leping Li, David M. Umbach, Paul Terry, Jack A. Taylor, Application of the GA/KNN method to SELDI proteomics data, Bioinformatics, Volume 20, Issue 10, 1 July 2004, Pages 1638–1640, https://doi.org/10.1093/bioinformatics/bth098

- Hong-Bin Shen, Jie Yang, Kuo-Chen Chou,Fuzzy KNN for predicting membrane protein types from pseudo-amino acid composition,Journal of Theoretical Biology,Volume 240, Issue 1,2006,Pages 9-13,ISSN 0022-5193,https://doi.org/10.1016/j.jtbi.2005.08.016.

- Olga Troyanskaya, Michael Cantor, Gavin Sherlock, Pat Brown, Trevor Hastie, Robert Tibshirani, David Botstein, Russ B. Altman, Missing value estimation methods for DNA microarrays , Bioinformatics, Volume 17, Issue 6, June 2001, Pages 520–525, https://doi.org/10.1093/bioinformatics/17.6.520

-  Jason Brownlee (October 24, 2019) Develop k-Nearest Neighbors in Python From Scratch. https://machinelearningmastery.com/tutorial-to-implement-k-nearest-neighbors-in-python-from-scratch/