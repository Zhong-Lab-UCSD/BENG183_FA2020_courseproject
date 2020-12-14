# Deep Learning in OMICS - Group 2

#### Fernando Bracamonte, Ishaan Gupta, Matias Lin

<!--lets update Contents after we're done finalizing the rest-->

## Contents

- [Introduction](#Introduction)
- [OMICS](#OMICS)
- [Deep Learning](#Deep-Learning)
  - [ANNs](#ANNs)
  - [Deep Learning Methods](#Deep-Learning-Methods)
  - [Applications](#Applications)
- [Conclusion](#Conclusion)
- [References](#References)

---

## Introduction

With the invention of new OMIC technologies, as well as with the advancement in technology withing new and old OMIC technologies, such as microarrays and next-generation sequencing, biological data has increased exponentially. These datasets are complex and would be nearly impossible for a human to extract valuable information from these in order to interpret it and make conclusions about it. Thus, this has given bioinformaticians and machine learning researchers a challenge to come up with ways to extract valuable information from these biological datasets to be able to fully analyze them. This has given rise to different deep learning algorithms and methods which are able to identify complex patterns and create predictive models and from these large biological datasets [(5)](#References).

### Aim of this lesson:

- To show how AI is revolutionizing Precision Medicine and OMICS data analysis
- To explain the background of Deep Learning and Artificial Neural Networks (ANNs), with a focus on Convolutional Neural Networks (CNNs)
- To introduce different kinds of architectures and appropriate uses
- To show what kinds of data can be used input and output for DL in OMICS data through examples
- Particularly focus on Variant Calling as an example application

---

---

## OMICS

Omics are the different science branches of Biology, which have the suffix of *-omics*, such as genomics (which is the focus of BENG 183), transcriptomics, epigenomics, metabolomics, proteomics, and so on [(8)](#References). Moreover, Omics represents al the different technologies that are used to determine the roles, relationships, and actions of different types of molecules for the structure, function and dynamic that make up the cells of an organism [(7)](#References).  A few Omic technologies are shown below with explanations as to what they study:

- Genomics: studies the structure, function, evolution, and mapping of genomes as well as the characterization and quantification of genes.
- Transcriptomics: studies the transcriptome, which is the collection of all mRNA
- Proteomics: studies all protein as well as their properties and functional roles 

With the summary of what some of these Omics technologies do, the overall objective of Omics as a whole is to identify, characterize and quantify all biological molecules that are involved in the structure, function and dynamics of a cell, tissue, or organism [(7)](#References). 


---

## Deep Learning Background

- Why DL is important
- AI, DL, ML, NN - Buzzword, for great reason, but meaning?
- AI: Andrew Moore, Former-Dean of the School of Computer Science at Carnegie Mellon University, “Artificial intelligence is the science and engineering of making computers behave in ways that, until recently, we thought required human intelligence.” [(1)](#References)
- ML: ML is a branch of AI. “Machine learning is the study of computer algorithms that allow computer programs to automatically improve through experience.” - Tom M. Mitchell, Carnegie Mellon University, Machine Learning Department [(1)](#References)
- DL networks are a class of ML algorithms uses ANNs
- ANNs are inspired by biological neural networks in a sense that they are formed by interconnected artificial neurons, which receive an input, apply a transformation to the data, and return an output
- DL can encode and learn from heterogeneous and complex data, in both supervised and unsupervised settings
  language processing, speech recognition, and image recognition
- In Omics data analysis: over-performed previous methods in terms of sensitivity, specificity and efficiency [(2)](#References)

### ANNs

#### Basic design:

- Image of a simple neural network
- Inputs are training data ($x$ for each training example), first layer outputs just that
- In the forward-propagation step, the outputs of activation function of neurons in one layer are successively applied weights and other parameters ($w,b$) on and fed to next layer in forward fashion. Output of final is the expected output ( $\hat{y}$ for each training example)
- Loss function ( $L(\hat{y},y)$ ) compares expected output with real output of training data ($y$ for each training example)
- Cost function $ J $ is the average of $L$ across all training examples.
- In back-propagation step, We use Gradient Descent to optimize Cost Function, i.e, find the parameters that minimize the Cost Function.
- In Gradient Descent, we change the parameters by a step proportional to the slope of Cost function for those parameters.
- So for each parameter $w$, $ \frac{\partial J}{\partial w} $ is computed by chain rule.
- Iteratively, we minimize $ J $ by iteratively in each forward propagation step (except initial) tuning the parameter $w$ in the direction $ -\frac{\partial J}{\partial w} $ This algorithm called gradient descent helps **learn** the parameters.

This is further complicated by use of various activation functions, differing the number of hidden layers, or the number of perceptrons in a layer, different ways to initialize the weights and other optimization techniques.
Furthermore, the example we saw is a Deep Feed-Forward NN (DFF), but there are different NN architectures specific to different uses.

### CNNs

If we want to use high dimensional data, such as images (with each pixel corresponding to a neuron in the input layer), as input for a neural network, we have a large number of neurons in the input layer and large number of neurons in the next layer. By the fully connected architecture we saw above, how many parameters would we need? Just the number of simple weights would the product of those two large numbers of neurons.

So for large data, we use Convolutional Neural Network Architecture (CNNs) that have layers themselves comprising of Convolutional filters and pooling layers, that act like feature reduction, reducing the number of parameters needed. Thus, CNNs are often used for DL with images.

![Convolution filter example](https://cdn.analyticsvidhya.com/wp-content/uploads/2018/12/Screenshot-from-2018-12-07-15-21-02.png)

###### Fig 1: Example of feature extraction with the help of Convolutional filter layer

![Pooling layer example](https://miro.medium.com/max/1400/1*-3-9b0tAakAsdozzhNlEww.png)

###### Fig 2: Example of feature extraction with the help of Pooling layer

Oncology is one of the areas in the medical field where CNNs are gaining prevalence. One of the papers that explored this possibility is "Convolutional neural networks can accurately distinguish four histologic growth patterns of lung adenocarcinoma in digital slides". To better improve the accuracy when diagnosing Lung Adenocarcinomas (LAC), researchers utilize DL to evaluate distinct histological tumor growth patterns [(9)](#References). There are five main growth patterns of interest when it comes to assaying LAC: Acinar (AC), Microcapillary (MP), Solid (SO), Cribriform (CR) and Non-Tumor (NT). In an effort to automate the task of quantifying these growth patterns, the scientists developed a pipeline that involves a CNN model.

![CNN Pipeline](./Images/cnn_hist_1.png)

###### Fig 3: Pipeline with a CNN model that classifies the different growth patterns in lung adenocarcinoma (LAC). A: Flow chart describing the model of CNN. B: Flow chart showing the whole pipeline of the project.

From Figure 3.A, we can observe that the researchers employ a convolutional neural network to predict all five growth patterns (AC, SO, MP, CR and NT) given an image (note that this paper refers to the input images as tiles). In this example, a single histopathology slide yielded 19,942 tiles corresponding to 5 classes and after data augmentation, 797,680 images were used to train the model. Once the CNN model was trained, it was incorporated into the overall pipeline as seen in Figure 3.B. The model is used to be able to classify the tiles to be able to quantify the different growth patterns and later construct the tumor growth pattern map.

Another interesting example involves the studying and diagnosis of breast cancer as described in the following paper: "Cancer diagnosis in histopathological image: CNN based approach". The process of diagnosing breast cancer is through the careful analysis of breast tissue cells. This is a task that can be wearisome and even error-prone if performed by an individual. Therefore, this paper proposes a machine learning approach where they use CNN models to predict whether a histopathology slide of breast tissue cells is malignant or benign [(10)](#References).

![BRCA Example](./Images/brca_pipeline.jpg)

###### Fig 4: Pipeline showing the use of CNN to predict whether a breast tissue cell is malignant or benign.

From Figure 4 we can that the CNN model will be able to take a histopathology slide of a breast tissue cell and classify it to be either malignant (label 0) or benign (label 1). The utilized a total of 7,909 biopsy images that were partitioned for training and testing, 6,327 and 1,582 respectively. After this model has been trained and tested, it reported the following performance: precision of 0.93, recall of 0.93, F1-Score of 0.93 and an accuracy of 0.98 [(10)](#References). These results suggest that the use of deep learning (CNN) not only resolves the laborious task of an classifying cells, but does so with impressive accuracy.

These papers not only demonstrate the potential of CNN in a clinical setting but also the wide range of applications in which this machine learning technique can be used in. We've seen in the first example how CNN could be used to classify different growth patterns in lung adenocarcinoma, and on the second example we've seen how a similar model could be used to predict whether a histopathology panel of breast tissue is malignant or not.

### RNNs and LSTMs

### Autoencoders

---

## Applications in OMICS and Precision Medicine

As previously explained, Deep Learning algorithms are good for the task of analyzing omics datasets. The workflow of Deep Learning applications in Omics data is depicted in Figure 5. The basic workflow is that deep learning algorithms/methods such as CNNs and RNNs are applied to biological data, such as sequencing data, alignment data, expression matrices, etc. From the output results of the deep learning methods, we get multiple applications, such as alternative splicing analysis, classification, enhancer prediction, varient calling, etc. Many of these applications also improve and give rise to precision medicine from analysing medical imagine to get a specific diagnosis for a person [(5)](#References). 

Some other examples of what deep learning applications can be used for are explained below:

### Genomics and Sequence analysis

There are many examples where deep learning methods have been applied to genomics data. One example is using CNNs which detects single-nucleotide polymorphisms (SNP) and indels. Another example is the use of DFFs and SAEs which predict the effect of genetic variants on gene expression. Finally, CNNs and LSTMs have been used to predict promoter sequences in genes, and CNNs have been used to identify splice junctions [(5)](#References). 

### Transcriptomics

### Epigenomics 

### Medical Imaging



![DL Applications in Omics](./Images/DLApplicationsOmics.jpg)

###### Fig 5: Workflow of Deep Learning Applications in Omics Data Analysis



### Applications of CNNs

<!--CNN for medical images here-->

An easy guess for an application might be using Medical images. For example,

OMICS application:
Detect SNPs/indels and other variants

---

### DeepVariant

#### Variant Calling

Variants are regions of the genome where the sequence differes from the reference genome. They could be in the form of:

- Single NUcleotide Variants (SNVs)
- Indels
- Structural Variants (SVs)
  - Copy number Variants (CNVs)
  - Translocation
  - Duplication
  - Inversion

![Variants types](Images/TypesOfVariants.png)

###### Fig 3: Types of Variants (6)

#### Pileups

#### Structure of DeepVariant Model

#### Comparison with other Variant Calling methods

### Other applications

## Conclusion

Conclusion...

---

### References

1. Machine Learning (ML) vs. Artificial Intelligence (AI) — Crucial Differences ( https://medium.com/towards-artificial-intelligence/differences-between-ai-and-machine-learning-and-why-it-matters-1255b182fc6 )
2. Deep learning in bioinformatics ( https://pubmed.ncbi.nlm.nih.gov/27473064/ )
3. A universal SNP and small-indel variant caller using deep neural networks ( https://pubmed.ncbi.nlm.nih.gov/30247488/ )
   full PDF: https://www.plantdna.cn/docs/july-1st/post1/poplin2018.pdf
4. Zhou J, Troyanskaya OG. Predicting effects of noncoding variants with deep learning-based sequence model. Nat Methods. 2015 Oct;12(10):931–4. [PMC free article] \[PubMed\]
5. Martorell-Marugán J, Tabik S, Benhammou Y, et al. Deep Learning in Omics Data Analysis and Precision Medicine. In: Husi H, editor. Computational Biology \[Internet\]. Brisbane (AU): Codon Publications; 2019 Nov 21. Chapter 3. Available from: https://www.ncbi.nlm.nih.gov/books/NBK550335/ doi: 10.15586/computationalbiology.2019.ch3
6. https://www.ebi.ac.uk/training-beta/online/courses/human-genetic-variation-introduction/what-is-genetic-variation/types-of-genetic-variation/
7. Ward, Sherry L. “Omics, Bioinformatics, Computational Biology.” AltTox.org, 14 July 2014, alttox.org/mapp/emerging-technologies/omics-bioinformatics-computational-biology/. Accessed 13 Dec. 2020.
8. Vailati-Riboni M., Palombo V., Loor J.J. (2017) What Are Omics Sciences?. In: Ametaj B. (eds) Periparturient Diseases of Dairy Cows. Springer, Cham. https://doi.org/10.1007/978-3-319-43033-1_1
9. Gertych, A., Swiderska-Chadaj, Z., Ma, Z., Ing, N., Markiewicz, T., Cierniak, S., Salemi, H., Guzman, S., Walts, A. E., & Knudsen, B. S. (2019, February 6). Convolutional neural networks can accurately distinguish four histologic growth patterns of lung adenocarcinoma in digital slides. Scientific Reports. https://www.nature.com/articles/s41598-018-37638-9?error=cookies_not_supported&code=1e50ee0c-b6fa-430e-bfd6-129301dc481c
10. Cancer diagnosis in histopathological image: CNN based approach. (2019, January 1). ScienceDirect. https://www.sciencedirect.com/science/article/pii/S2352914819301133 (#10)
