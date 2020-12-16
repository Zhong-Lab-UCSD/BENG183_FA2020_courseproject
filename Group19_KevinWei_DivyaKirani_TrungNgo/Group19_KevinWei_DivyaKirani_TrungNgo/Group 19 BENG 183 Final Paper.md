# <div align="center">Tailed Testing and Designing of a Hypothesis</div>

## **Introduction**
Before we get into all the details of how to construct a hypothesis for tailed tests, let’s begin with the basic process of the **scientific method**.

## **Scientific Method**
The scientific method is an empirical method of acquiring knowledge that has characterized the development of science since at least the 17th century.<sup>[[1]](https://www.khanacademy.org/science/high-school-biology/hs-biology-foundations/hs-biology-and-the-scientific-method/a/the-science-of-biology)</sup>

**It involves the following general steps:**
* Make an **observation**
* Ask a **question**
* Form a **hypothesis** or testable prediction
* **Test** the prediction
* **Conclude** experiment
* **Report** Results

### <div align="center">**Figure 1.1 Scientific Method**<sup>[[2]](https://s3-us-west-2.amazonaws.com/courses-images/wp-content/uploads/sites/2569/2017/10/23192123/1000000000000342000002C90F1084BF.png)</sup></div>
<div align="center"><img src="Figure 1.1.JPG" width="450" /></div>

As we can see, forming a hypothesis is a crucial step in a scientific experiment, it projects our understanding of the things that we are trying to explore and the possibilities behind it. 

## **What is a hypothesis?**
A hypothesis is a supposition or **proposed** explanation made on the basis of **limited** evidence as a starting point for **further investigation**. The keywords here are “proposed”, “limited”, and “further investigation”. Just like the word “hypothesis” itself, a hypothesis is less (hypo-) than a theory (-thesis). It is an idea we propose with limited evidence that awaits further investigation. 

To convert an idea to a hypothesis, the idea must have testable predictions. Here are two examples to be considered:

1. Mint chocolate chip ice cream tastes better than strawberry cheesecake ice cream.
2. At UC San Diego, the mean of undergraduate students that would rather have mint chocolate chip ice cream as their dessert is GREATER than that of strawberry cheesecake ice cream.

As we can see, the first example is rather a subjective proposal. But other than that, it does not provide a cue for us to test it; thus it is NOT a hypothesis. However, the second example, it asserts the possible relationship between the means of each population. We can collect the test statistics by surveying people at UCSD about their preferences on their dessert given these two options. It is testable and experimental; thus, it is a hypothesis.

## **Null vs Alternative Hypothesis**
Hypothesis testing involves the careful construction of two **competing** statements: the null hypothesis and the alternative hypothesis.<sup>[[3]](https://www.thoughtco.com/null-hypothesis-vs-alternative-hypothesis-3126413)</sup>

## **The Null Hypothesis** 
The null hypothesis reflects that there will be no observed effect in our experiment. This hypothesis is denoted by H0. The null hypothesis is what we attempt to find evidence against in our hypothesis test. We hope to obtain a small enough p-value that it is lower than our significance level, subjective to study, and we are justified in rejecting the null hypothesis. If our p-value is greater than the significance level, then we fail to reject the null hypothesis.

Just like in court, if a person has been declared "not guilty" during a legal verdict, it does not mean that they are innocent because there is a lack of evidence. Similarly, if the null hypothesis is not rejected, we cannot state that the null hypothesis is accepted. However, in the case of rejection of the null hypothesis, we can accept the alternative hypothesis.

For example, if we are studying a new treatment, the null hypothesis is that our treatment will not affect our subjects’ health in any significant way. In other words, the treatment will not significantly affect our subjects.

## **The Alternative Hypothesis** 
The alternative or experimental hypothesis reflects that there is an observable  relationship for our experiment. This hypothesis is denoted by either Ha or by H1.

The alternative hypothesis is what we are attempting to demonstrate by the experiment. If the null hypothesis is rejected by the experiment, then we accept the alternative hypothesis. If the null hypothesis is not rejected, then we do not accept the alternative hypothesis. 

Using the above example, if we are studying a new treatment, the alternative hypothesis is that our treatment will improve our subjects’ health. 

## **Experimental Results** 
Once we have competing hypotheses, we need to categorize experimental results into a statistical dataset to test whether the null hypothesis needs to be rejected or not. Based on, but not limited to, the following factors, we can choose a specific statistical test and conclude our experiment. 
1. The type of data
2. The size of each of the samples
3. The independence of the samples in the experiment
4. The distribution of the samples
5. The outcome we hope to achieve from the experiment

## **Data Types** 
The type or format of data and the size of our dataset from our experiment is critical to choosing a test. The below list/flowchart represents the different types of data.<sup>[[4]](https://blog.minitab.com/blog/understanding-statistics/understanding-qualitative-quantitative-attribute-discrete-and-continuous-data-types)</sup>

### <div align="center">**Figure 1.2 Different Data Types**</div>
<div align="center"><img src="Figure 1.2.JPG" width="550" /></div>

**Quantitative data:** Data that is in the form of numerical values and can be measured objectively. Examples: Height, Weight
* Discrete data: Data is stratified or in the form of categories
* Continuous data: Data is progressive and has minute increments 

**Qualitative data:** Data that is not in the form of numerical values and is measured subjectively. Examples: Preference of ice cream
* Binary data: Data that can be divided into two categories that are disjoint and exclusive. 
* Unordered data: Data formed from categorizing samples that are not naturally ranked. 
* Ordered data: Data formed from categorizing samples that have some natural rank.

## **Forming a Test Statistic** 
To conduct a statistical test to determine whether or not the null hypothesis can be rejected, a test statistic is required to provide support to one of the two competing hypotheses. To create a test statistic, one first needs a statistic which must be a single number that utilizes the tested data points. To call it a test statistic, it must be an arbitrary variable that helps form an argument or show support for one side. 

To demonstrate making an argument using a test statistic:

We are looking at the effects of wearing anti-blue ray glasses on eye fatigue after looking at a screen for a fixed amount of time. Here, we are contrasting the fatigue level of sample A with that of sample B. Sample B is the same population wearing the glasses. 

A sample test statistic for this could be the number of individuals from each population set that experience eye fatigue. The mean or median number derived from each dataset will provide an argument in favor of one hypothesis.

## **Introduction to the Statistical Test**
After categorizing the experimental results, we can find an appropriate statistical method to understand the probability of whether the outcome of an experiment is true.<sup>[[5]](http://osp.mans.edu.eg/tmahdy/papers_of_month/0706_statistical.pdf)</sup>
 
Here are some of the basic, common layers to a statistical test. These layers are stacked upon each other to discover an appropriate statistical method to conclude if the experiment is correct. 

It is important to note that some tests do not include the following layers or may be referred to with different terms. A one-size fits all rule does not apply.

### <div align="center">**Figure 1.3 Common Layers of Statistical Testing**</div>
<div align="center"><img src="Figure 1.3.JPG" width="500" /></div>

*The statistical test that makes use of all 3 common layers and prevalent in this chapter, is the Student’s T-test.*

### **Outer layer: Parametric or Non-parametric testing**
Parametric testing is dependent on the existence of parameters. There are three main differences between parametric and non-parametric tests<sup>[[5]](http://osp.mans.edu.eg/tmahdy/papers_of_month/0706_statistical.pdf)</sup>:

### <div align="center">**Figure 1.4 Parametric vs. Non-Parametric**</div>
<div align="center"><img src="Figure 1.4.JPG" width="550" /></div>
Due to these requirements, we often use non-parametric tests in conjunction with parametric tests within the same experiment. This allows us to cover different aspects of the same experiment or different types of data. 

### **Middle layer: Paired or Unpaired Testing**
Paired or unpaired testing is used based on the samples in our experiment. If we are using the same population which has changed over time, we use a paired test.<sup>[[10]](https://www.statisticshowto.com/probability-and-statistics/t-test/#PairedTTest)</sup> The two samples are **“dependent”** of each other and we need to analyze the difference. If we are using two separate populations with the same method applied, we use an unpaired test. These two samples are **“independent”** of each other and we need to analyze the individual samples.

### **Bottom layer: One-tailed or Two-tailed Testing**
One and two-tailed testing is specific to t-tests. In one-tailed testing, our t-distribution has only one rejection region. In the case of two-tailed testing, the rejection region is halved into two regions.<sup>[[6]](https://stats.idre.ucla.edu/other/mult-pkg/faq/general/faq-what-are-the-differences-between-one-tailed-and-two-tailed-tests/)</sup> Let us take the above example on anti-blue ray glasses to show this. 

*Case 1: One-tailed test* \
Our first sample or sample A is the population without the anti-blue ray glasses. Our second sample **consists of the same people** from sample A with the anti-blue ray glasses. If we want to examine whether the eye fatigue levels after looking at a screen **increases**, we need to use a **paired, one-tailed test**. This is because we are seeing how wearing anti-blue ray glasses **increases** the eye fatigue levels of the same set population over time.

*Case 2: Two-tailed test* \
Our first sample or sample A is the population without the anti-blue ray glasses. Our second sample **consists of the same people** from sample A who are now wearing the anti-blue ray glasses. If we want to examine whether the eye fatigue levels after looking at a screen **changes**, we need to use a **paired, two-tailed test**. This is because we are seeing how wearing anti-blue ray glasses only **affects** the eye fatigue levels of the same set population over time. 

**Hypotheses for Tailed Testing**
* One-tailed testing: We analyze whether the mean or median of a one sample is greater than or less than the other one
* Two-tailed testing: We analyze whether the mean or median of a sample is simply different

The following set of formulations involving the mean/median of the samples may help when you are drafting your null and alternative hypotheses.

**One-tailed:** \
Null hypothesis: “A is equal to B.” Alternative hypothesis “A is less than B.”\
Null hypothesis: “A is equal to B.” Alternative hypothesis “A is greater than B.”

### <div align="center">**Figure 1.5 One-tailed Testing Distribution**<sup>[[6]](https://stats.idre.ucla.edu/other/mult-pkg/faq/general/faq-what-are-the-differences-between-one-tailed-and-two-tailed-tests/)</sup></div>
<div align="center"><img src="Figure 1.5.JPG" width="450" /></div>

**Two-tailed:** \
Null hypothesis: “A is equal to B.”\
Alternative hypothesis: “A is not equal to B.”

### <div align="center">**Figure 1.6 Two-tailed Testing Distribution**<sup>[[6]](https://stats.idre.ucla.edu/other/mult-pkg/faq/general/faq-what-are-the-differences-between-one-tailed-and-two-tailed-tests/)</sup></div>
<div align="center"><img src="Figure 1.6.JPG" width="450" /></div>

Please refer to the below figure if interested in other statistical tests<sup>[[7]](http://abacus.bates.edu/~ganderso/biology/resources/statistics.html)</sup>:

### <div align="center">**Figure 1.7 Different Statistical Test**</div>
<div align="center"><img src="Figure 1.7.JPG" width="450" /></div>

*Extra Note(Fig 1.7): In the previous examples related to anti-blue ray glasses, we are looking for whether there is a **difference** between the two samples. If we wished to understand whether there is a **correlation** between blue rays and eye fatigue to begin with, we could use correlative or regression analyses.*

Although each test has its own requirements and limitations, the type of test we use is mainly based on the data and the experimental outcomes we want to analyze. This affects how we test our hypotheses. 

Since the focus of our textbook chapter is tailed testing, after forming our null and alternative hypotheses, we can conclude our experiment based on the p-value.

## **Finding the P-value**
The p-value can show the probability of finding a set of observations or more extreme observations when the null hypothesis is true.<sup>[[8]](https://online.stat.psu.edu/statprogram/reviews/statistical-concepts/hypothesis-testing/p-value-approach)</sup> The test statistic is an arbitrary variable and its value is based on the experimental results. The p-value is **1 minus the probability distribution of the test statistic when the null hypothesis is true**. In a one-tailed test, it's to the right of this distribution while for a two-tailed, it's split amongst the left and right.

### <div align="center">**Figure 1.8 Example R Script for P-Value Calculation (t-test)**<sup>[[11]](https://www.cyclismo.org/tutorial/R/pValues.html#calculating-a-single-p-value-from-a-normal-distribution)</sup></div>
<div align="center"><img src="Figure 1.8.JPG" width="450" /></div>

## **Drawing Conclusions**
After calculating the p-value for the applicable tests, the value can be used to determine the strength of belief against the null hypothesis. The most general significance level used in most scenarios is 5% where if the p-value is less than this value, the test rejects the null hypothesis. If the p-value is greater than 5%, the test fails to reject the null hypothesis. The smaller the p-value, the greater the improbability of the data with the null hypothesis. 

## **Learning Goals:**
* Understand the scientific method
* Differentiate between null and alternative hypothesis
* Data Types and Test Statistic
* Common Characteristics of Statistical Testing
    * Parametric vs Nonparametric
    * Paired vs Unpaired
    * One-tailed vs two-tailed
* Concluding Experiment for Hypothesis with Tailed Testing


## **References** 
[1]: https://www.khanacademy.org/science/high-school-biology/hs-biology-foundations/hs-biology-and-the-scientific-method/a/the-science-of-biology \
[2]: https://s3-us-west-2.amazonaws.com/courses-images/wp-content/uploads/sites/2569/2017/10/23192123/1000000000000342000002C90F1084BF.png \
[3]: Taylor, Courtney. "Null Hypothesis and Alternative Hypothesis." ThoughtCo, Aug. 27, 2020, thoughtco.com/null-hypothesis-vs-alternative-hypothesis-3126413 \
[4]: https://blog.minitab.com/blog/understanding-statistics/understanding-qualitative-quantitative-attribute-discrete-and-continuous-data-types \
[5]: http://osp.mans.edu.eg/tmahdy/papers_of_month/0706_statistical.pdf \
[6]: https://stats.idre.ucla.edu/other/mult-pkg/faq/general/faq-what-are-the-differences-between-one-tailed-and-two-tailed-tests/ \
[7]: http://abacus.bates.edu/~ganderso/biology/resources/statistics.html \
[8]: https://online.stat.psu.edu/statprogram/reviews/statistical-concepts/hypothesis-testing/p-value-approach \
[9]: Lecture and Example Class Handout - https://github.com/Irenexzwen/Applied-Genomic-Technologies/blob/master/statistics_cheatsheet.pdf \
[10]: https://www.statisticshowto.com/probability-and-statistics/t-test/#PairedTTest \
[11]: https://www.cyclismo.org/tutorial/R/pValues.html#calculating-a-single-p-value-from-a-normal-distribution