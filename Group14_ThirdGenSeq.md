# Third Generation Sequencing

## Overview

### Brief History of Second-Generation Sequencing

Following the explosion of second-generation sequencing technology in the early 2000s (also referred to as next-generation sequencing or NGS), researchers' ability to produce genetic data at a high throughput with a manageable cost greatly increased. The commercialization of these technologies by biotech companies such as Illumina allowed large scale genome construction and powerful analyses which were unfeasible with first-generation Sanger sequencing techniques.

The increase in throughput was due in large part to massively parallelizing sequencing reactions. The rapid development of bioinformatics tools allowed processing and analyzing the huge amounts of data outputted by second-generation sequencing technologies. However, second-generation sequencing was severely limited in terms of read-length, allowing fragments of only several hundred base pairs in length. This causes complications for genome assembly as this process is inherently more difficult with shorter reads. All aspects of genome construction and analysis are affected by read length due to the probabilistic nature of recombining fragments, with short reads inevitably leading to inaccuracies, especially in areas with high amounts of repeats or copy number variations. These limitations led to more companies developing novel technologies beginning in the late 2000s and throughout the 2010s. 

### What is Third-Generation Sequencing?

Third-generation sequencing, for the purposes of this discussion, will be defined as long-read, single molecule sequencing without the need for amplification of the genetic material. These technologies, therefore, remove the amplification necessary for second-gen sequencing, and allow much longer read lengths, reducing the complications in gemone assemply inherent to second-generation techniques. 

### Early Third-Generation Technologies: Helicos

The earliest technique relevant to third-generation sequencing is Helicos’ sequencing technology. Originally developed in the Stephen Quake Lab, this technology grew into Helicos as a company. The company (now defunct) attempted to utilize a similar method of sequencing to Illumina, featuring dyed nucleotides which are imaged before being cleaved, and the sequencing proceeding nucleotide by nucleotide. Helicos, however, did not use bridge amplification in their process, working directly with non-amplified DNA samples. This technology was unable to achieve success in the long term, but it can be considered the first step in third-generation sequencing. 

<img src="https://urldefense.com/v3/__https://i.imgur.com/pDusI4k.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo9SsJ-af$ " width="40%">

### Pacific Biosciences and SMRT sequencing

Following this, technologies which achieved more long-term success began to be developed, starting with Pacific Biosciences' SMRT sequencing technology. SMRT, standing for single molecule real time sequencing, uses a DNA polymerase and fluorescent nucleotides in their sequencing process, which will be described in depth in the following section. This novel DNA sequencing technology allowed for significantly longer reads, often of lengths roughly 10kb. This significantly longer read length, as well as avoiding the need for DNA amplification, makes this technology popular for some sequencing and genome assembly projects. An issue facing PacBio, however, is the high error rate of their sequencing methods for single reads, but this is an area of active development.

<img src="https://urldefense.com/v3/__https://i.imgur.com/pfVGza6.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo9AMUYwA$ " width="40%">

### Nanopore Sequencing Technology and Oxford Nanopore

The other major company and method currently being used in third-generation sequencing is Oxford Nanopore Sequencing. Nanopore sequencing is the newest development in third-generation sequencing and features the use of nanopores to process DNA molecules, which will be discussed in further detail below. The technology is still being actively developed, but already features a number of unique advantages. The record length for a single molecule genetic read is currently held by Oxford Nanopore’s technology at an astounding 2 Mbp, with most Oxford Nanopore users reading fragments in the tens of thousands of base pairs. Additionally, Oxford Nanopore is developing sequencing devices which are portable, in some cases as small as a USB stick. These features provide unique possibilities for genome assembly as well as the ability to sequence genetic data in a variety of locations and circumstances due to the portability of the technology. 

Other companies such as Quantapore and Stratos are developing their own unique sequencing technologies centered around the use of nanopores. However, as of now, the most prevalent third-gen technologies in are PacBio's SMRT sequencing and Oxford Nanopore Sequencing technology. These two technologies and their methodology will be discussed in depth in the following sections. 

## PacBio(SMRT Sequencing)

SMRT Sequencing stands for Single-Molecule Real Time Sequencing. The key idea is to be able to sequence one long dsDNA molecule, ~10kb, without the need for multiple reads or alignment to a reference genome. The figure below outlines the general workflow of SMRT Seq, covered in more detail below.

<img src="https://urldefense.com/v3/__https://i.imgur.com/622TprK.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo58OX9WM$ " width="50%">

SMRT Seq was introduced by the company PacBio, whose sequencing workflow consists of the following key steps:

### Step 1:  Fragment the DNA into sequences of ~10kb

SMRT Seq is beneficial because it can sequence fragments longer than the typical 200bp sequences second-gen sequencing takes in. However, there is still a limit to the DNA sequence length SMRT Seq can process, which is around 10kb. Therefore, it is important to fragment the target DNA sequence into appropriate lengths. 

### Step 2: Add adaptors to the DNA fragments to form the SMRTbell template

Once the DNA fragments are the right length, hairpin adaptors are added to the both ends of the fragment. This is shown in the image below where the green loop-like structures ligated to each end of the dsDNA are the adaptors. Ligation of these adaptors forms a circular structure which is called the SMRTbell template. 

<img src="https://urldefense.com/v3/__https://i.imgur.com/hVbe8OD.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo4R_71KI$ " width="40%">

### Step 3: SMRTbell template is loaded onto the SMRT cell 

Like the Illumina flow cell, SMRT Seq also utilizes what is known as a SMRT cell where DNA fragments can bind to be sequenced. Each SMRT cell contains about 500,000 Zero Mode Waveguides (ZMWs). ZMWs are wells which provide the smallest available volume for light detection and allow the SMRTbell template to diffuse. Each ZMW has DNA polymerase anchored to the bottom of the cell which can then bind to either of the hairpin adaptors on the DNA fragment for sequencing. 

<img src="https://urldefense.com/v3/__https://i.imgur.com/sWDy8Ve.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo7at7o4A$ " width="30%">

### Step 4: Sequencing through light pulse and color emission

Once the SMRTbell diffuses into a ZMW, DNA polymerase binds to one of the hairpin adaptors. The actual sequencing process is similar to Illumina Sequencing where fluorescently tagged nucleotides are added to synthesize a complementary strand. Each of the four nucleotides is tagged with a unique fluorescent dye (G is red, C is yellow, T is green, and A is blue) giving each nucleotide its own emission spectrum. During sequencing, polymerase holds the nucleotide in the detection volume, and a light pulse is emitted. The resulting fluorescence color output is used to identify the base. The dye-linker-pyrophosphate product is then cleaved off of the nucleotide terminating the fluorescence pulse and allowing polymerase to move to the next nucleotide and continue the cycle. 

The two images below illustrate the sequencing process. The image on the left shows polymerase anchored to the bottom of a ZMW. In this specific moment, the light pulse is causing an emission color of yellow, corresponding to a Cytosine base being added.

The image on the right illustrates the process of a fluorescently dyed nucleotide being added to the synthesized complementary sequence. Cytosine associates with the active site of polymerase and is held in place while the pulse identifies the base. Then, the dye-linker-pyrophosphate is cleaved allowing polymerase to move to the next position. 

<img src="https://urldefense.com/v3/__https://i.imgur.com/s0ylQ5P.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo-xq2ITy$ " width="75%">

Overall, each of the pulses produced from one ZMW can be interpreted as a sequence of bases which contribute to one Continuous Long Read (CLR). This is ultimately how SMRT Seq can process and sequence long fragments in real time. Although this method of sequencing seems foolproof, there are certain advantages and disadvantages that scientists must consider when deciding whether to utilize this technology. We go into comparisons between NGS and third-generation sequencing more below, however it is important to note a few key advantages and disadvantages of SMRT Seq. Because this technology can sequence very long DNA fragments at one time, it is beneficial when sequencing repeat regions which NGS has more difficulty with. On the other hand, SMRT Seq is very low throughput and the error rate can be quite high which is also very important to consider. 

## Nanopore Sequencing (Oxford Nanopore)

### Nanopore anatomy/basics

A nanopore is a hole with a diameter of only a few nanometers situated in a membrane. A single DNA strand of practically unlimited length can be sequenced as it passes through the nanopore. The two main types of nanopores include biological and solid-state nanopores.

#### Biological nanopores

Biological nanopores consist of a naturally-occuring pore-forming protein situated in a biological membrane such as a lipid bilayer. These proteins can be produced by inserting their genetic sequences into a bacterial genome. Three of the most common proteins used for sequencing are α-hemolysin, MspA, and bacteriophage phi29. The main advantages of biological nanopores include:
1. Consistency: Protein structure is entirely defined by the genetic sequence used to produce it, leading to highly reproducible results.
2. Modifiability: Specific amino acid residues in the protein can be changed using modern genetic engineering techniques.
Commercial nanopore sequencing products today, including Oxford Nanopore’s MinION, GridION, and PromethION flow cells, use biological nanopores.

<img src="https://urldefense.com/v3/__https://i.imgur.com/VA1fzVz.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo8D5Fh6M$ " width="60%">

Macromolecular structure of α-hemolysin, the first and most commonly used biological nanopore.

#### Solid-state nanopores

Solid-state nanopores are created by puncturing synthetic membranes such as silicon nitride, silicon dioxide, or graphene. Many different techniques have been used for creating solid-state nanopores, including focused ion or electron beams.
Synthetic nanopore creation is not yet precise enough to be used commercially, but the potential advantages include: 
1. Adjustable pore size: Unlike biological nanopores, where the diameter is restricted by the protein, solid-state nanopores of varying size can be made. 
2. Stability: Solid-state nanopores are more chemically, thermally, and mechanically stable than biological nanopores, and can be used under a wider variety of experimental conditions.
3. Low cost: Solid-state nanopores have the potential to be mass-produced at a lower cost and timeframe than biological nanopores.

### Mechanics

<img src="https://urldefense.com/v3/__https://i.imgur.com/SotS2xt.jpg__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo92JJPCO$ " width="50%">

1. Double-stranded RNA or DNA strands are prepared by attaching a motor protein and an adapter to the end of the sequence.
2. A voltage bias is applied across the membrane, inducing ion flow through the nanopore.
3. When the DNA/motor protein compound approaches the nanopore, the negatively-charged DNA is drawn towards the opening. The motor protein locks into the nanopore.
4. The motor protein splits the DNA, allowing one strand to pass through the nanopore while the other strand stays on the original side of the membrane. The motor protein also controls the speed at which the strand passes through the membrane, with the speed being 450 bp/sec for each DNA strand sequenced by MinION, GridION, or PromethION flow cells.
5. As the negatively charged DNA molecule passes through the nanopore, it disrupts the ion current. Different DNA base sequences cause characteristic disruptions in the current These disruptions are recorded in real-time, and converted to DNA sequence since different bases cause characteristic disruptions in the current. 

### Sequencing

<img src="https://urldefense.com/v3/__https://i.imgur.com/lBTC5Xs.png__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo90_3XUG$ " width="50%">

The narrowest section of the nanopore protein is called the ‘reader’ and is long enough for 4 DNA bases. Each sequence of 4 bases is associated with a particular disruption in the ion current. As the DNA strand moves through the nanopore, the ion current disruption is read in real time and a recurrent neural network algorithm is used to translate this signal into a base sequence. The DNA sequence output can be viewed in real time, which is a feature unique to nanopore sequencing. 
Nanopore sequencing also has several other key advantages over competing technologies, including NGS and PacBio sequencing, discussed in more detail below.

## Comparisons/Conclusions

This table describes many of the features of Illumina Technology as well as both PacBio and Oxford Nanopore’s third-generation techniques:

<table>
  <tr>
   <td>
   </td>
   <td><strong>Next-Gen Seq</strong>
<p>
<strong>(Illumina)</strong>
   </td>
   <td><strong>Third-Gen Seq</strong>
<p>
<strong>(PacBio)</strong>
   </td>
   <td><strong>Third-Gen Seq</strong>
<p>
<strong>(Oxford Nanopore)</strong>
   </td>
  </tr>
  <tr>
   <td><strong>Read length</strong>
   </td>
   <td>200 bp
   </td>
   <td>~10 kb
   </td>
   <td>>10 kb
   </td>
  </tr>
  <tr>
   <td><strong>Error rate</strong>
   </td>
   <td>~0.1-1%
   </td>
   <td>~11-15% per run
   </td>
   <td>~10% per run
   </td>
  </tr>
  <tr>
   <td><strong>PCR Amplification</strong>
   </td>
   <td>Required
   </td>
   <td>Not required
   </td>
   <td>Not required
   </td>
  </tr>
  <tr>
   <td><strong>Key advantages</strong>
   </td>
   <td>Accurate
   </td>
   <td>Fast run time,
<p>
long reads
   </td>
   <td>Fast, portable,
<p>
long reads,
real-time output
   </td>
  </tr>
</table>

1. Read Length

Illumina’s next generation technology provides reads of several hundred bases in length, while both third-generation techniques offer reads on the scale of 10kB, with Oxford Nanopore having had a record read of as large as 2.3 Mbp.

2. Error Rate

Illumina’s technology has a low error rate and offers highly accurate sequencing information. Both third-gen techniques face the issue of having high error rates for their technologies on a single read, a limitation which both methods are working to address as they develop their technology. 

3. PCR Amplification

While Illumina’s method requires amplification of samples, third-generation technologies, by their definition, do not require this step, avoiding some of the challenges and issues which come with amplification, but also requiring the DNA samples being used to be of high quality. 

4. Summary of Comparisons

Illumina and next-gen sequencing are widely used and powerful technologies renowned for their proven effectiveness and accuracy in sequencing. Third-generation technologies provide significant advantages in terms of read length and development of portable, real-time methods for sequencing. While third-generation sequencing still has far lower accuracy than next-gen sequencing, recent advances have drastically reduced error rates (from ~30% to ~10% for nanopore technologies). With increased accuracy reducing the need to read the same DNA sequence multiple times, third-generation technologies may offer long read length combined with high throughput which is unprecedented in the industry. 

## References

1. Daber, Robert, et al. “Understanding the Limitations of Next Generation Sequencing Informatics, an Approach to Clinical Pipeline Validation Using Artificial Data Sets.” Cancer Genetics, Elsevier, 28 Nov. 2013, https://urldefense.com/v3/__http://www.sciencedirect.com/science/article/pii/S2210776213001609__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo5XQm7ZU$ . 

2. Feng, Yanxiao, et al. “Nanopore-Based Fourth-Generation DNA Sequencing Technology.” Genomics, Proteomics & Bioinformatics, Elsevier, 2 Mar. 2015, https://urldefense.com/v3/__http://www.sciencedirect.com/science/article/pii/S1672022915000133__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo8l6JjZF$ . 

3. Giani, Alice Maria, et al. “Long Walk to Genomics: History and Current Approaches to Genome Sequencing and Assembly.” Computational and Structural Biotechnology Journal, Elsevier, 17 Nov. 2019, https://urldefense.com/v3/__http://www.sciencedirect.com/science/article/pii/S2001037019303277__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo8_Y2mMM$ .

4. Heather, James M., and Benjamin Chain. “The Sequence of Sequencers: The History of Sequencing DNA.” Genomics, Academic Press, 10 Nov. 2015, https://urldefense.com/v3/__http://www.sciencedirect.com/science/article/pii/S0888754315300410__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvow1eQqTa$ . 

5. “Nanopore Sequencing: Making the Promise a Reality”. Quantapore. Quantapore, 2018. Web. https://urldefense.com/v3/__https://quantapore.com/__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo2EmVeji$ 

6. Oxford Nanopore Technologies. “Introduction to Nanopore Sequencing.” YouTube, 2 Apr. 2020, https://urldefense.com/v3/__http://www.youtube.com/watch?v=sv9fFeSd3kE&ab_channel=OxfordNanoporeTechnologies__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo_vQ8oG9$ . 

7. “Resource Centre”. Oxford Nanopore. Oxford Nanopore, 2018. Web. https://urldefense.com/v3/__https://nanoporetech.com/resource-centre/most-complete-human-genome-ever-assembled-single-technology*:*:text=More*20recently*2C*20researchers*20from*20the,entire*204*20Mb*20MHC*20region__;I34lJSUlJSUlJSU!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvox2g2Tr3$  

8. Rhoads, Anthony, and Kin Fai Au. “PacBio Sequencing and Its Applications.” Genomics, Proteomics & Bioinformatics, Elsevier, 2 Nov. 2015, https://urldefense.com/v3/__http://www.sciencedirect.com/science/article/pii/S1672022915001345__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo35Ad4kn$ . 

9. “SMRT Sequencing - PacBio - Highly Accurate Long-Read Sequencing.” PacBio, 1 Dec. 2020, https://urldefense.com/v3/__http://www.pacb.com/smrt-science/smrt-sequencing/__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvoyjbM6jj$ . 

10. Stratos Genomics. Stratos Genomics Inc., 2018. Web. https://urldefense.com/v3/__https://www.stratosgenomics.com/__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo1D9AltI$  

11. “Template Preparation and Sequencing Guide”. Pacific Biosciences. Pacific Biosciences, 2014. Web. https://urldefense.com/v3/__https://www.pacb.com/wp-content/uploads/2015/09/Guide-Pacific-Biosciences-Template-Preparation-and-Sequencing.pdf__;!!Mih3wA!VOKYPqrmTKln4AekxjK4kKshB6E-9_1kiB5A7vS422_4OMWYFypzNTKvo6AX9E66$ 

12. “Types of Nanopores.” Oxford Nanopore Technologies, 14 Apr. 2020, nanoporetech.com/how-it-works/types-of-nanopores. 

13. Xiao, Tiantian, and Wenhao Zhou. “The third generation sequencing: the advanced approach to genetic diseases.” Translational pediatrics vol. 9,2 (2020): 163-173. doi:10.21037/tp.2020.03.06

