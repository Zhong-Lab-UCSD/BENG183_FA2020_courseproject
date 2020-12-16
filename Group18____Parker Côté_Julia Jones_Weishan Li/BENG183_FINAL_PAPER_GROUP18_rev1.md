# Algorithms behind Spliced Transcript Alignment to a Reference  

*Group 18: Parker Côté, Julia Jones, Weishan Li*

*BENG 183 FA2020 Final Paper*
---

#### STAR (Spliced Transcript Alignment to a Reference) is a efficient read mapping algorithm that handles RNA-Seq libraries

With the rapid development of sequencing technology and the need for sequencing coverage, modern RNA-Seq experimental runs can easily generate libraries between 30~200 million reads.

The sheer size of the read libraries and the non-continuous nature of RNA-Seq reads overwhelms traditional RNA-Seq aligners, which suffer from slow runtime and high alignment error rates. STAR overcomes all of these challenges with the combination of the seed and extend approach and the fast string search algorithm.

---

### Why do we care about alignment speed and mapping error?
Modern computers are fast, with billions of transistors switching on and off at a rate of several gigahertz. However, the computation power we have is easily dwarfed by the size of input we wish to analyze. Given the length of genomes, even algorithms running in polynomial runtime can take an impractical time to execute.   


#### How bad is the Naïve approach?
The naïve string search algorithm is simple. The query string slides over the reference text and char-by-char comparisons are made after each slide. [5]



This approach works quite well for small inputs, but careful inspection of its execution reveals lot of unnecessary work. For instance: Try aligning AAAB to reference AAAAAAAAAA

```
1-1	⌄		1-2      ⌄		1-3	  ⌄		1-4	   ⌄		
	AAAAAAAAAA		AAAAAAAAAA		AAAAAAAAAA		AAAAAAAAAA
	AAAB			AAAB			AAAB			AAAB
	⌃		         ⌃		          ⌃		           ⌃				  		

2-1	 ⌄		2-2       ⌄		2-3	   ⌄		2-4	    ⌄		
	AAAAAAAAAA		AAAAAAAAAA		AAAAAAAAAA		AAAAAAAAAA
	 AAAB			 AAAB			 AAAB			 AAAB
	 ⌃			  ⌃		           ⌃	                    ⌃			

...

7-1	      ⌄		7-2            ⌄	7-3	        ⌄	7-4	         ⌄		
	AAAAAAAAAA		AAAAAAAAAA		AAAAAAAAAA		AAAAAAAAAA
	      AAAB		      AAAB		      AAAB		      AAAB
	      ⌃			       ⌃		        ⌃		         ⌃
```
Notice that the algorithm repeatedly compares the first 3 "A"s in the query to the reference, only to arrive at the last "B" and realize the alignment at the current position fails. Eventually, the program will terminate after 28 total single-char comparisons.

For a reference text is 10 chars long and the query 4 chars long, do we really need to do more than 10 comparisons to be able to confidently report the alignment status?  

The answer is no. A slightly improved version of the naïve string search, the KMP algorithm, reduces the number of comparisons by "remembering" what was previously compared and achieves linear time in the worst case. That is, any character in the reference will not be compared with the query in more than one sliding position. [6]


However, when the input is millions of short reads and whole genomes, however, linear time is still considered too slow.



#### Mapping error

**Mapping error** typically occur when a RNA-Seq read spans the alternatively spliced junctions and one segment of the read is ambiguously assigned to multiple exons. [7] 

Some aligners before STAR used the **split-read** approach. The read sequences are first split into smaller fragments, either based on prior knowledge of the junction site or certain preliminary continuous alignment results, and then are individually aligned. The issue of **mapping error** can arise from incomplete annotation of the target transcriptome, biasing the alignment towards the known exons over the unknown ones. 



#### What is an example of an actual, practical alignment tool? 

After discussing the shortcomings of the naïve approach, it is now time to talk about an example of an alignment tool that is actually used in industry. 

**BLAST**, or the **(Basic Local Alignment Search Tool)**, is probably "the most widely bioinformatics tool every written". [1] It is typically used to align a query of protein sequence to some transcriptome database, and has the capacity to handle alignment between protein sequences and DNA sequences given a transcription frame. 

The algorithm behind **BLAST** is the **Aho-Corasick Automaton**, a dictionary-matching algorithm that locates a collection of patterns (queries) in the reference text (a database of DNA or protein sequences). The algorithm uses the "trie" data structure to align multiple patterns within linear search time with respect to the database size.  

In a nutshell, the Aho-Corasick algorithm transforms the set of patterns to a trie, where characters of patterns serve as paths that connects one node to another. The reference is run against the trie, and whenever the reference text contains a pattern of interest, that specific permutation of characters "navigates" itself to a destination node that signifies the algorithm of a match. 

The explanation is in itself abstract and hard to understand, but hopefully the below example of searching amino acid patterns *ql, zl, ln, lb, nf* in database *qlnfs*, visualization credit [8] , illustrates the concept better.  

![](https://github.com/wel268/BENG183_FA2020_courseproject/blob/main/Group18____Parker%20C%C3%B4t%C3%A9_Julia%20Jones_Weishan%20Li/ACT.gif?raw=true)


---

### STAR Strategy
The efficient mapping of STAR is achieved through a 2 step process:


#### 1. Seed Search


**Maximal Mappable Prefix** (**MMPs**), sometimes more simply referred to as **seeds**, are segments of the RNA-Seq reads that exactly match to the reference genome. [3] STAR begins from the first base of the read sequence and extracts the segment that continuously matches to the genome. When a junction is hit, the continuous mapping terminates and a discrete **seed** is thus produced. The seed finding process is continued on the remainder of the unmapped reads, until the read is depleted.  

The seed search component of STAR is implemented as uncompressed **Suffix Array** (SA), which takes logarithmic time with respect to the size of genome.   


#### 2. Clustering, Stitching and Scoring

The "seeds" generated by seed search must be clustered, and "stitched" across gaps in order to produce the final alignments. The output also needs to be scored

1. In **Clustering**, **Anchor alignments** are used to facilitate the combination of seeds in proximity. **Anchor alignments** are alignments that map to some small, user defined value (typically between 20 to 50).

   Seeds near these **anchors** are clustered together to yield the best *linear complete alignment*.

2. In **Stitching**, clusters across gaps (splice junctions) are matched together. A complicated scoring function is rolled over the genomic region between clusters to optimize for the start and end of splice junctions and is implemented through **dynamic programming** to yield linear runtime. [4]

3. **Scoring** is based on mismatches, indels, gaps and other genomic features that indicate *distance*. The user is able to define the quantity of penalties for each of the features. 


---


### Suffix Array (SA)
**Suffix Array** is a data structure that enables for fast string/pattern search. 

It is introduced by Manber and Myers as an space efficient alternative to the **suffix tree**.  

In STAR, the reference text (in context of RNA-Seq, the genome) is first converted to a suffix array and stored as a text file. 


#### Representing substrings with integers 

Consider the length 14 genome AGCTGCATTACCGT, we initialize an array of of the size of that genome, and fill in the array element as integers 1 thru 14. 

| 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   | 11   | 12   | 13   | 14   |

The Array itself is rather uninteresting, but given the definition: 

Each **i**-th **index** represents the **i**-th **suffix**, which is a **substring** of the genome, starting at the **i**-th character and extending till the end of the genome. 

The array of integers now contains the information charted in the table below. 

| Index | i-th position in original genome | Represented Substring (w/o strike-through) |
| ----- | -------------------------------- | ------------------------------------------ |
| 1     | **A**GCTGCATTACCGT               | AGCTGCATTACCGT                             |
| 2     | A**G**CTGCATTACCGT               | ~~A~~GCTGCATTACCGT                         |
| 3     | AG**C**TGCATTACCGT               | ~~AG~~CTGCATTACCGT                         |
| 4     | AGC**T**GCATTACCGT               | ~~AGC~~TGCATTACCGT                         |
| 5     | AGCT**G**CATTACCGT               | ~~AGCT~~GCATTACCGT                         |
| 6     | AGCTG**C**ATTACCGT               | ~~AGCTG~~CATTACCGT                         |
| 7     | AGCTGC**A**TTACCGT               | ~~AGCTGC~~ATTACCGT                         |
| 8     | AGCTGCA**T**TACCGT               | ~~AGCTGCA~~TTACCGT                         |
| 9     | AGCTGCAT**T**ACCGT               | ~~AGCTGCAT~~TACCGT                         |
| 10    | AGCTGCATT**A**CCGT               | ~~AGCTGCATT~~ACCGT                         |
| 11    | AGCTGCATTA**C**CGT               | ~~AGCTGCATTA~~CCGT                         |
| 12    | AGCTGCATTAC**C**GT               | ~~AGCTGCATTAC~~CGT                         |
| 13    | AGCTGCATTACC**G**T               | ~~AGCTGCATTACC~~GT                         |
| 14    | AGCTGCATTACCG**T**               | ~~AGCTGCATTACCG~~T                         |

Notice that each **i-th** suffix is just a **substring** of the genome, starting at the **i-th** character and extending till the end. The actual substrings are there for demonstration purposes, all information a suffix array contains can be represented with one copy of the genome and the numerical array (So the computer does not have to store all the repeated strings). 


#### Sorting suffixes 

To make the Suffix Array actually useful for string search, we need to **sort** it. Sorting of strings that are up to certain lengths and with a fixed alphabet system is typically done through **lexicographical** ordering system. The idea behind **lexicographical ordering** is that, given a x character alphabet system and a fixed length n, there will be at most x^n unique strings we can construct. And with some **combinatorics** magic we can define a **one-to-one and onto function** that maps every string to a integer between 1 and x^n (or 0 and x^n-1). We can then compare the strings like we compare integers. 

For convenience of illustration, we will drop the lexicographical order and simply define that: 

                                                 A<T<C<G

* When comparing 2 strings, we simply proceed to the first character position that the strings differ at and apply the above rule (e.g. AA < AT < AC < AG). If one of the strings is an exact prefix of the other, then the shorter string is considered smaller (e.g. A < AC < ACT < ACTG).  
* If one string is an exact prefix of the other (e.g. ATC is a prefix of ATCGG), then the shorter string is considered smaller (e.g. A < AC < ACT < ACTG).  


If we implement the rule as the comparator, we can use that to sort the suffix array. 

With the fastest sorting algorithm, the sorting of the suffix index is typically done in **O(N*Log(N)) **time, where **N** is the length of the genome. This runtime may not sound great, but realize that generating the suffix index for a set of genome is an one time investment -- as soon as the index are sorted and stored, you may align as many sequences to the index as you like with high speed.   

| Index | Original-Index | Represented Substring |
| ----- | -------------- | --------------------- |
| 1     | 7              | ATTACCGT              |
| 2     | 11             | ACCGT                 |
| 3     | 1              | AGCTGCATTACCGT        |
| 4     | 14             | T                     |
| 5     | 9              | TACCGT                |
| 6     | 8              | TTACCGT               |
| 7     | 4              | TGCATTACCGT           |
| 8     | 6              | CATTACCGT             |
| 9     | 3              | CTGCATTACCGT          |
| 10    | 11             | CCGT                  |
| 11    | 12             | CGT                   |
| 12    | 13             | GT                    |
| 13    | 5              | GCATTACCGT            |
| 14    | 2              | GCTGCATTACCGT         |


#### Searching in Suffix Array

The sorted **Suffix Array** is now ready to handle string search tasks 

Since the array is in sorted order, we can now use **binary search** to quickly navigate to the position of query string in the array. The principle behind binary search is that the query is compared to the middle element of a sorted array to eliminate half of the search range -- If the search element is larger than the middle element, the first half of the array will be dropped, and smaller, the second half dropped. 

Below is an example of searching string CGT in the genome with **binary search** in SA

![alt](https://github.com/wel268/BENG183_FA2020_courseproject/blob/main/Group18____Parker%20C%C3%B4t%C3%A9_Julia%20Jones_Weishan%20Li/BinarySearch.gif?raw=true)

By the property of **binary search**, with each string to string comparison of query against the middle suffix, we reduce our search range by half, and thus in the worst case we need **O(Log(N))** of string to string comparisons to reduce the search range to 1, at which point we can easily determine whether the query is found or not. 

In each string comparison we do at most as many single character comparisons as the length of our query string. Thus we may accomplish any search task in **O(Log(N)M)** single-char comparisons, where M is the string size and N is the genome size

---

### Pros and Cons of STAR
#### Pros:
1. **Alignment time complexity** O(log(N)M): This is much *faster* than the naïve string search method due to the underlying suffix array used in searches

1. **Ability to handle indels and mismatches**: The naïve method can only handle exact matches and these features are very common in the RNA data that STAR deals with. Because of their prevalence, *exact matches are not always required for biological data to be relevant*.

#### Cons:
1. **Memory Intensive**: Since we access the text through binary search, the entire genome needs to be kept in RAM. This is very memory intensive considering the size of the average genome STAR will handle.


---

### Running STAR 

**Installing STAR**

With anaconda, installing STAR is as simple as running the command below.

```
conda install star
```

We can check to see if STAR has successfully installed (and learn about using STAR) with the following command:

```
STAR -h
```

STAR is also included within many popular bioinformatics packages for Python such as bioconda and may already be installed as a part of one of these packages.

**Generate Suffix Array from Reference Genome**

Before we can begin aligning our reads, we must first use STAR to generate a suffix array from our reference genome. The command below can be used to achieve just that.

```
STAR --runThreadN 10 --runMode genomeGenerate
--genomeDir /path/to/output
--genomeFastaFiles /path/to/input/FASTA_file
--sjdbGTFfile /path/to/input/GTF_file --sjdbOverhang 100     
```

`--runThreadN`: Number of threads to use  

`--runMode`: STAR run mode to use, for this application we use genomeGenerate 

`--genomeDir` : The path for STAR to output to

`--genomeFastaFiles` : The path to reference genome FASTA file

`--sjdbGTFfile` : The path to reference genome GTF file

`--sjdbOverhang` : Typically we use read length - 1

This step will usually take a couple of minutes to complete, so be patient.

**Align Reads to Reference Genome**

Once the Suffix Array has been generated from our reference genome, the command below will map our reads to the reference.

```
STAR --runThreadN 10
--genomeDir /path/to/output
--readFilesIn /path/to/input/FASTQ_file
--outSAMtype BAM SortedByCoordinate
--outFileNamePrefix prefix_for_output_files
```

`--runThreadN`: Number of threads to use

`--genomeDir`: The path for STAR to output to

`--readFilesIn`: The path to FASTQ file containing our reads

`--outSAMtype`: For our purposes (RNA-Seq), we typically use BAM SortedByCoordinate

`--outFileNamePrefix`: The prefix for our output file names

This step requires a significant amount of computer resources in order to complete and may be unable to complete on poorly equipped computers.

**Our Results**

In our output directory we will have several new files, with the most important files being the final log file and the sorted BAM file. The final log file (with the suffix Log.final.out) will contain important information regarding the quality of our alignment including the total mapping ratio, unique mapping ratio, etc. The sorted BAM file (with the suffix Aligned.sortedByCoord.out.bam) will be used along with featureCounts in following step of the RNA-Seq bioinformatics pipeline, expression quantification. 

---
### Sources
1. [http://www.mi.fu-berlin.de/wiki/pub/ABI/AlignmentHeuristicsWS11/blast-filtering.pdf](http://www.mi.fu-berlin.de/wiki/pub/ABI/AlignmentHeuristicsWS11/blast-filtering.pdf)
2. [https://hbctraining.github.io/Intro-to-rnaseq-hpc-O2/lessons/03_alignment.html](https://hbctraining.github.io/Intro-to-rnaseq-hpc-O2/lessons/03_alignment.html)
3. [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3530905/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3530905/)
4. [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3530905/bin/supp_29_1_15__index.html](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3530905/bin/supp_29_1_15__index.html)
5. [https://www.geeksforgeeks.org/naive-algorithm-for-pattern-searching/?ref=lbp](https://www.geeksforgeeks.org/naive-algorithm-for-pattern-searching/?ref=lbp)
6. [https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/?ref=lbp](https://www.geeksforgeeks.org/kmp-algorithm-for-pattern-searching/?ref=lbp)
7. [https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4863231/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4863231/)
8. [http://jovilab.sinaapp.com/visualization/algorithms/strings/aho-corasick](http://jovilab.sinaapp.com/visualization/algorithms/strings/aho-corasick)

