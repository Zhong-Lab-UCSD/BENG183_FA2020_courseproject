![chip_seq pipeline](./images/Intro.png)
# CHIP-Sequencing and Potential Improvement
BENG183 Final Paper <br>
Date: 12-15-2020<br>
Group 4: Kelly Chou, Renyi Zhao, Li Yu Tang<br>


1. [Introduction](#1)
2. [ChIP-Sequencing Workflow](#2)<br>
    2.1 [Experimental Workflow](#21)<br>
    2.2 [Computational Analysis](#22)<br>
3. [Advantages](#3)
4. [Disadvantages](#4)
5. [Improved Methodologies](#5)<br>
    5.1 [Limited Cell Number](#51)<br>
    5.2 [ChIP-exo](#52)<br>
    5.3 [Re-ChIP](#53)<br>
6. [Quality Control](#6)<br>
    6.1 [Sequencing Depth](#61)<br>
    6.2 [S/N - The Signal To Noise Ratio](#62)<br>
7. [References](#7)


## 1. Introduction<a name="1"></a>


<p align="center">
  <img src="./images/Workflow.jpg">
</p>

ChIP-Sequencing stands for chromatin-immunoprecipation and focuses on protein-DNA interactions. It uses antibodies to select specific proteins or nucleosomes that are then hybridized to a microarray to identify the DNA fragments later. It enriches for DNA fragments bound to proteins or nucleosomes.

The goal of ChIP-Sequencing is to map binding sites of any DNA binding protein, histone modifications, nucleosome positioning, and other protein-DNA interactions.

---

## 2. ChIP-Sequencing Workflow<a name="2"></a>

### 2.1 Experimental Workflow<a name="21"></a>


<p align="center">
  <img src="./images/experimental.png" width="500" height="400"/>
</p>

1. **Crosslink**

The proteins are first crosslinked to the DNA using formaldehyde.

2. **Shear Chromatin**

Then, the chromatin is sheared into smaller pieces by sonication or enzymes to digest them.

3. **Add protein-specific antibody**

Next, the antibodies for the specific protein in question is added.

4. **Immunoprecipitation**
Later, the DNA is immunoprecipitated to isolate and concentrate the particular protein in question.

5. **Purify DNA**
The crosslinks are reversed and the DNA is purified using the antibody-bound magnetic beads.

6. **Prepare for sequencing**

The immunoprecipitated DNA is now prepared to be used for a next-generation sequencing to be analyzed for DNA binding sites.


### 2.2 Computational Analysis<a name="22"></a>
<p align="center">
    <img src="./images/computational.jpg">
</p>

After the DNA is prepared for sequencing and mapping, different analysis strategies may be used depending if there is a **small-scale analysis**, like a single or small sample, or a **large-scale anaylsis** with many samples. Normally **differential analysis** is used for small-scale samples with **spike-in analysis** or **de novo normalization** by using different [signal-to-noise (S/N) ratios](#61) and underlying assumptions. For small-scale analyses, **peak-calling strategies** and parameters may be adjusted. For large-scale analyses, it may be wise to **jointly analyze** all the ChIP samples instead of comparing peaks for each sample individually. A **relaxed threshold** to compare the peaks may be used for large-scale analyses.

**Peak calling** is comparing different peaks from each experiment. There are three modes that each require different peak-calling strategies: 
- **sharp mode**: specific positions in genome
- **broad mode**: large genomic domains
- **mixed mode**: both specific positions and large genomic domains

Broad and mixed mode peaks are associated with weak and widespreach enriched regions with no clear peak summits and sequence specficity.

In addition, other analysis strategies may be used to further analyze: 
- **Functional analysis**: motif analysis, gene ontology
- **Integration with other technologies**: gene expression, chromatin, genetic variation, DNA methylation
- **Validation**: qPCR, knockdown analysis

---

## 3. Advantages<a name="3"></a>
- **Mapping**

    It can be used to map DNA-binding proteins and histone modifications in a genome-wide manner at base-pair resolution.
    
- **Higher resolution, less noise, higher genome coverage and wider dynamic range**

- **Requires few amounts of DNA**
    
    Generates a more precise list of protein binding sites and targets of transcription factors, enhancers, and identification of sequence motifs. Detailed profiling of           histone modifications and nucleosome positions enables greater understanding of epigenetic mechanisms in development and differentiation.
 
- **Repetitive regions in the genome can now be examined**

- **Increased sensitivity and specificity**

    Increased sensitivity and specificity in the mapping of transcription factor binding sites can facilitate motif discovery and target identification.
    
- **Compatibility with various input of DNA samples.**

- **Single nucleotide resolution**

    While the resolution for ChIP-chip varied by arrays, it is generally in the range of 30-100 bp.
    
- **Eliminate signal noise**

    During ChIP-chip’s hybridization process there may be cross-hybridization between imperfectly matched sequences, which adds to signal noise. ChIP-seq is intrinsically         immune to such sources of noise due to the direct sequencing method.


---

## 4. Disadvatages<a name="4"></a>
- **High cost and availability**

    ChIP-chip costs $400–$800 per array (1–6 million probes) but multiple arrays may be needed for large genomes, however ChIP-Seq cost around $1000–$2000 per Illumina lane       (6–15 million readsprior to alignment)

- **High quality of antibodies required**

    ChIP-seq makes use of antibodies in immunoprecipitation, hence the quality of the data relies on the high quality of the antibody. However, antibodies vary widely in           quality between suppliers and batches.

- **Required large amounts of tissue**

    It requires a lot of tissue to be prohibitive for some rare sample types. The peaks in the profiles need to be compared to the same loci of the control sample to make        the result more accurate.

- **Prior knowledge of DNA-binding protein required**

    Prior knowledge of specific binding sites are needed for the antibodies to see where they exactly bind to the protein that we are interested in. 
    
- **Bias in high GC-rich content in fragment selection**


---

## 5. Improved Methodologies<a name="5"></a>
### 5.1 Limited Cell Number<a name="51"></a>
### 5.2 ChIP-exo <a name="52"></a>
### 5.3 Re-ChIP  <a name="53"></a>
---
## 6. Quality Control<a name="6"></a>
### 6.1 Sequencing Depth<a name="61"></a>
The number of called peaks increases with the sequencing depth, because the weaker sites become statistically significant with a greater number of reads. Thus, the number of called peaks increas as the sequencing depth increases. Sufficient sequencing depth is required to include all functional sites, which avoids the technical biases caused by uneven Chip-enrichment. A saturation analysis is usually performed to determine adquate sequencing depth. And for most histone-modification which exists no clear saturation point, the depth is usually determined empirically. <br>
Increased sequencing depth allows detection of more sites with reduced enrichment. <br>
It is noted that setting a minimal signal strength threshold, usually based on a p-value or false discovery rate calculation, to identify peaks does not guarantee discovery of all functional sites. It is also noted that DNA sequencing library complexity, that is the amount of unique DNA molecules, must be sufficient meaning sequencing depths do not exceed complexity. It is suggested that at least 80% of 10 million or more reads be mapped to distinct genomic locations. Low complexity libraries generally indicate a failed experiment where not enough DNA was recovered causing the same PCR amplified products to be sequenced repeatedly and many small peaks to be detected with a high false positive rate.

### 6.2 Signal To Noise Ratio S/N <a name="62"></a>


---
## 7. References<a name="7"></a>
1.  Barski, A., & Zhao, K. (2009, January 27). Genomic location analysis by ChIP‐Seq. Retrieved December 07, 2020, from https://onlinelibrary.wiley.com/doi/pdf/10.1002/jcb.22077
2.  Furey, T. (2012, December). ChIP-seq and beyond: New and improved methodologies to detect and characterize protein-DNA interactions. Retrieved December 07, 2020, from https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3591838/
3.  Nakato, R., & Sakata, T. (2020, March 30). Methods for ChIP-seq analysis: A practical workflow and advanced applications. Retrieved December 07, 2020, from https://www.sciencedirect.com/science/article/pii/S1046202320300591
4.  Nakato, R., & Shirahige, K. (2017, March 1). Recent advances in ChIP-seq analysis: From quality management to whole-genome annotation. Retrieved December 07, 
2020, from https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5444249/


---

# Text weight

# Really heavy text!
## Less heavy
### Even littler
#### I'm shrinking
##### Oh no
###### plz help
This is some normal text...

This is a new paragraph
that continues in the same line despite the line break.


---


# Text formatting

 **I'm bold!**

 *I'm italic!*

### <span style="color:cyan">COLOR!</span> <span style="color:red">COLOR!</span> <span style="color:yellow">COLOR!</span> <span style="color:magenta">COLOR!</span>



---

# Links
## [I'm a hyperlink](https://en.wikipedia.org/wiki/YOLO_(aphorism)
[*I'm a small italic link*](https://en.wikipedia.org/wiki/YOLO_(aphorism)

___


# Quoting

"Normal Quotes"

Block quotes!

>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Mauris a ipsum nec justo dictum convallis. Integer luctus ultricies tortor sit amet vehicula. Nam tristique faucibus pharetra. Cras nec erat ligula. Proin at odio ex. Nulla ornare imperdiet nulla, sed posuere est imperdiet et. Curabitur egestas risus vitae quam pulvinar, in vulputate leo mollis. Fusce nec tincidunt libero. Suspendisse odio urna, pretium eget lectus id, accumsan bibendum ex. Aenean accumsan malesuada sem, at blandit dui euismod a. Sed sed eros porttitor, iaculis augue id, pulvinar mi. Ut in scelerisque libero, quis malesuada sem. Donec commodo diam quis massa condimentum, non consequat orci bibendum. Praesent auctor tellus egestas felis tincidunt, eget imperdiet lorem pharetra.

---

# Pictures
Two ways to format this
![Puppy0](https://www.merriam-webster.com/assets/mw/images/article/art-wap-landing-mp-lg/puppy-3143-ad4140d8f6055cda2cd8956d4af37ea9@1x.jpg "A puppy!")


![Puppy1][puppy2]

[puppy2]: https://i.ytimg.com/vi/AZ2ZPmEfjvU/maxresdefault.jpg "Another Puppy!!"


[![Puppy2](https://pbs.twimg.com/profile_images/446566229210181632/2IeTff-V_400x400.jpeg "This puppy is a link!")](nytimes.com)

---

# Code
You can reference variables like `x` or `y` inline.
But you can also have block quotes like:
```
import numpy as np
random = np.random.randn(10, 10)

print('Hello World!')
```
But you can even format the text for languages:
```python
import numpy as np
random = np.random.randn(10, 10)

print('Hello World!')
```
**Pretty!**


----

# Lists

1. Item One
2. Another


* Unordered Item
* Another one!

---

# Tables
Note the different alignments

|Time of day| Favorite snack | Why?                |
|-----------|:----------------:|----:              |
|Morning    | Oreos!           | Delicious         |
|Afternoon  | Otter Pop        | It's hot out baby |
|Night      | IPA              | I need it. |

# Comments (look at the source code)

[comment]: <> (This is a comment
               everything in here won't be in the final doc)

 <!---
This is also a comment :)
 -->
