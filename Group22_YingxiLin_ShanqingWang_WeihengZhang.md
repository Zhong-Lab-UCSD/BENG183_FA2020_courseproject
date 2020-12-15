# KNN Algorithm
#### BENG183 Group 22 
#### Yingxi Lin, Shanqing Wang, Weiheng Zhang

## What is KNN?
KNN stands for K-nearest neighbors. It is one of the most basic supervised machine learning algorithm. In principles, it can be used for both classification and regression, but in practice, it is more often used in classification. The algorithm makes predictions based on similarities determined from the features. 
For example, in this image below, we are trying to classify fruit, there are three classes and the features here are sweetness and sourness. So if we want to classify a new fruit, we would classify it to one of these three classes based on its sour and sweet level.

![](https://i1.wp.com/radacad.com/wp-content/uploads/2017/03/fruit.png)

## How does the algorithm work?
Let now talk more in depth about how this algorithm actually works. First we would need to have some training data. Because this is a supervised algorithm, the data needs to be labeled. Then we try to choose an appropriate k, which we will talk about later.
To predict a new unlabled data point d, we would calculate the distances between d and each point in the training set. Next we will rank these distances from the shortest to the longest and select the top k nearest neighbors to vote on the prediction of the new data point d. If it is regression, we would compute the average of the neighbors's labels and if it is classification, we would compute the mode of the neighber's labels. It is essentially a majority voting situation.
Here is an visualzaiton of what I just talke about. So here we have two classes, green triangle and red star. And we have these labeled data points. Now we want to use this model to predict this new question mark data point. So we would first compute the distances between this question mark and all the labeled data point. Since k=3, we would select the closes three neighbors, and in this case we have two green and oen red, so we would classify this unknown data point as green.

![](https://res.cloudinary.com/dyd911kmh/image/upload/f_auto,q_auto:best/v1531424125/KNN_final1_ibdm8a.png)
## How to fine tune the model?

## Prerequisites of KNN
We cannot use KNN on whatever data we get. There are certain prerequisites on the dataset to make sure KNN can run correctly.

Firstly, we need to make sure all samples are correctly labelled. For the KNN question in our midterm 2 exam, if all healthy patients are mislabeled as having cancer AB, then our calculation will be ruined. For samples missing label or having incorrect label, we should either fix them or discard them. 

Secondly, we need to make sure our dataset is clean. We should try to get rid of noise and outliers in the dataset. If we are trying to predict male and female from height and weight, samples labelled as “bio major” should not exist. We need to discard samples with extreme values because KNN is very sensitive to outliers and will produce inaccurate classification. Thus, for the samples with red colored labels and numbers in the following chart, we should either fix their value or discard them. 

![](http://i2.tiimg.com/572075/46ec849b7c21dbff.png)

We also need to make sure our dataset is balanced, which means the dataset should contain similar amount of “male” and “female” samples in this case. If only 1% of all the samples are male then KNN’s result will not be effective. 


Lastly, the dataset cannot contain too many samples, and each sample cannot have too many features. Because KNN is a lazy algorithm without training step, it does not produce a discriminative function on the training data. If the dataset contains too many samples, calculating distances between query point and the whole dataset would be very computational heavy. High dimensionality in the dataset will also greatly impact both the performance and accuracy of KNN.


## Advantages and Disadvanage of KNN
Nothing is perfect. KNN algorithm has its strength and weaknesses. 
### Pros
* KNN is very easy to learn. You can code your own from scratch in almost any programming language. 
* Does not require training step at all. Directly use the given dataset for prediction.
* Above features makes it very easy to be implemented on new problems. 
* Because KNN can do both classification and regression, it is powerful on a wide range of use cases. 

### Cons
* Lazy algorithm. Does not produce a discriminative function. Prediction speed is slower than other non-lazy algorithms. 
* Big dataset or samples with high dimensionality greatly impact KNN's performance.
* Sensitive to unclean dataset. Require a pre data check to get rid of noise, outliers and data imbalance. 
* Users need to know how to choose a good k. A bad k value will ruin the accuracy. 




## Example use case
KNN has been used in different bioinformatics application:
- Mining high-dimensional microarray gene expression data (Li et.al.)
- Predicting membrane protein type (Shen et.al)
- Estimating missing data from DNA microarray (Troyanskaya et.al.)
## Refererences
- Hastie, Trevor. (2001). The elements of statistical learning : data mining, inference, and prediction : with 200 full-color illustrations. Tibshirani, Robert., Friedman, J. H. (Jerome H.). New York: Springer.

- Huang, Ru & Gao, Lei. (2018). Identification of potential diagnostic and prognostic biomarkers in non-small cell lung cancer based on microarray data. Oncology Letters. 15. 10.3892/ol.2018.8153. 

- N. S. Altman (1992) An Introduction to Kernel and Nearest-Neighbor Nonparametric Regression, The American Statistician, 46:3, 175-185, DOI: 10.1080/00031305.1992.10475879

- Simplilearn. KNN Algorithm Using Python | How KNN Algorithm Works | Data Science For Beginners | Simplilearn. YouTube, 6 June 2018, www.youtube.com/watch?v=4HKqjENq9OU.

- Srivastava, T. (2020, October 18). K Nearest Neighbor: KNN Algorithm: KNN in Python & R. Retrieved from https://www.analyticsvidhya.com/blog/2018/03/introduction-k-neighbours-algorithm-clustering/

- Leping Li, David M. Umbach, Paul Terry, Jack A. Taylor, Application of the GA/KNN method to SELDI proteomics data, Bioinformatics, Volume 20, Issue 10, 1 July 2004, Pages 1638–1640, https://doi.org/10.1093/bioinformatics/bth098

- Hong-Bin Shen, Jie Yang, Kuo-Chen Chou,Fuzzy KNN for predicting membrane protein types from pseudo-amino acid composition,Journal of Theoretical Biology,Volume 240, Issue 1,2006,Pages 9-13,ISSN 0022-5193,https://doi.org/10.1016/j.jtbi.2005.08.016.

- Olga Troyanskaya, Michael Cantor, Gavin Sherlock, Pat Brown, Trevor Hastie, Robert Tibshirani, David Botstein, Russ B. Altman, Missing value estimation methods for DNA microarrays , Bioinformatics, Volume 17, Issue 6, June 2001, Pages 520–525, https://doi.org/10.1093/bioinformatics/17.6.520