# BENG183_FA2020_courseproject

#Group2

## Members

* Fernando Bracamonte
* Ishaan Gupta
* Matias Lin


## Contents
- [Introduction](#Introduction)
- [OMICS](#OMICS)
- [Deep Learning](#Deep-Learning)
  * [ANNs](#ANNs)
  * [Deep Learning Methods](#DL-Mehods)
  * [Applications](#Applications)
- [Conclusion](#Conclusion)
- [References](#References)

---


## Introduction

### Aim of this lesson:
- To show how AI is revolutionizing Precision Medicine and OMICS data analysis
- To explain how DL neural network works through example of basic architecture
- To introduce different kinds of architectures and appropriate uses
- To show what kinds of data can be used input and output for DL in OMICS data through examples
- Particularly focus on Variant Calling as an example application

---

## OMICS

OMICS...


---

## Deep Learning Background
- Why DL is important
- AI, DL, ML, NN - Buzzword, for great reason, but meaning?
- AI: Andrew Moore [6] [36] [47], Former-Dean of the School of Computer Science at Carnegie Mellon University, “Artificial intelligence is the science and engineering of making computers behave in ways that, until recently, we thought required human intelligence.” [1]
- ML: ML is a branch of AI. “Machine learning is the study of computer algorithms that allow computer programs to automatically improve through experience.” -  Tom M. Mitchell, Carnegie Mellon University, Machine Learning Department [1]
- DL networks are a class of ML algorithms uses ANNs
- ANNs are inspired by biological neural networks in a sense that they are formed by interconnected artificial neurons, which receive an input, apply a transformation to the data, and return an output
- DL can encode and learn from heterogeneous and complex data, in both supervised and unsupervised settings
language processing, speech recognition, and image recognition
- In Omics data analysis: over-performed previous methods in terms of sensitivity, specificity and efficiency [2]

### ANNs

#### Basic design: 

- Image of a simple neural network
- Inputs are training data ($x$ for each training  example), first layer outputs just that
- In the forward-propagation step, the outputs of activation function of neurons in one layer are successively applied weights and other parameters ($w,b$)   on and fed to next layer in forward fashion. Output of final is the expected output ( $\hat{y}$ for each training example)
- Loss function ( $L(\hat{y},y)$ ) compares expected output with real output of training data ($y$ for each training example)
- Cost function is the average of $L$ across all training examples.
- In back-propagation step, for each parameter $w$, $ \frac{\partial J}{\partial w} $ is computed by chain rule.
- Iteratively, we minimize $ J $ by iteratively in each forward propagation step (except initial) tuning the parameter $w$ in the direction $ -\frac{\partial J}{\partial w} $ This algorithm called gradient descent helps **learn** the parameters.

This is further complicated by use of various activation functions, differing the number of hidden layers, or the number of perceptrons in a layer, different ways to initialize the weights and other optimization techniques.
Furthermore, the example we saw is a Deep Feed-Forward NN (DFF), but there are different NN architectures specific to different uses. 

### CNNs
If we want to use high dimensional data, such as images (with each pixel corresponding to a neuron in the input layer), as input for a neural network, we have a large number of neurons in the input layer and large number of neurons in the next layer. By the fully connected architecture we saw above, how many parameters would we need? Just the number of simple weights would the product of those two large numbers of neurons.

So for large data, we use Convolutional Neural Network Arcgitecture (CNNs) that have layers themselves comprising of Convolutional filters and pooling layers, that act like feature reduction, reducing the number of parameters needed. Thus CNNs are often used for DL with images.

![Convolution filter example](https://cdn.analyticsvidhya.com/wp-content/uploads/2018/12/Screenshot-from-2018-12-07-15-21-02.png)
###### Fig 1: Example of feature extraction with the help of Convolutional filters
Medical images application
OMICS application:
Detect SNPs/indels and other variants


## Applications

---
### DeepVariant

#### Variant Calling

##### Pilups

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
4. Zhou J, Troyanskaya OG. Predicting effects of noncoding variants with deep learning-based sequence model. Nat Methods. 2015 Oct;12(10):931–4. [PMC free article] [PubMed]


