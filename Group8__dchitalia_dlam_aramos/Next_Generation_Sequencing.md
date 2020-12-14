# In Depth Look at Next Generation Sequencing

## Library Preparation

The library preparation step of next generation sequencing is essential for a successful next generation sequencing run. These initial steps ensure that issues with the quality of the sequencing reads and purity of the DNA samples do not affect the results of the run as well as making sure Illumina's sequencing analysis algorithms are able to perform downstream without issues. In this section, we will take a closer look at all the steps involved in a standard Illumina next generation sequencing library preparation. 

### Workflow
![](./img/Lib_Prep_Workflow.png)
This image shows a general view of the NGS library preparation workflow. It includes:
- The addition of Illumina's sequencing by synthesis adaptors
- A first magnetic bead purification
- The addition of Illumina's index sequences
- A second magnetic bead purification
- A DNA quantification step
- A sample dilution and addition of PhiX control
- A sequencing run

We will now take a closer look at each one of these steps

### PCR 1: Addition of SBS Adaptors and Purification 1
#### Sequencing by Synthesis Adaptors
![](./img/SBS_Sequences.png)
[Illumina SBS Adaptors](https://www.illumina.com/documents/products/techspotlights/techspotlight_sequencing.pdf)

The Illumina sequencing by synthesis adaptors are the first set of sequences to be added to the sample DNA. These adaptors are important because they allow the DNA samples to bind on to the flow cell surface and eventually are used to conduct bridge amplification in the sequencing workflow. These adaptors are added by polymerase chain reaction and then the samples are purified.
#### Magnetic Bead Purification 1
![](./img/Bead_Purification.png)
[Bead Purification](https://mvspacific.com/REAGENTS/DNA%20Isolation%20Kits.htm)

After the first PCR, the DNA samples will be contaminated with a variety of PCR residues and DNA dimers that can potentially affect the sequencing run. In order to purify these samples, a magnetic bead purification is done. This process involves:
- Adding magnetic beads to bind to the DNA samples of interest
- Placing the sample on a magnet to isolate the DNA samples that are bound to the beads
- Removing the contaminants from the solution
- Eluting the DNA from the beads

### PCR 2: Addition of Index Sequences and Purification 2
#### Index Sequences
![](./img/Index_Sequences.png)
[Illumina Index Sequences](https://www.researchgate.net/figure/Dual-index-PCR-primers-designed-for-paired-end-Illumina-sequencing-of-5-UTR-region-The_fig5_289734765)

The addition of Illumina's unique dual (UD) index adaptors allows each sample of DNA to be identified after the sequencing run. These adaptors usually come in pairs (i5 and i7) and are 10 bases long. The addition of these adaptors makes it possible for scientists to conduct massively parallel sequencing runs with many different samples placed into a single pool. This technology saves time and the cost of having to conduct each of these sample sequencing runs in separate pools. Further downstream, the Illumina analysis algorithms are able to separate the sequences of the different samples in the pool by identifying the unique indexes. The addition of these indexes are done by a second PCR which, again, requires a purification.

#### Magnetic Bead Purification 2
After the second PCR, the DNA samples must be purified again in the exact same way they were purified after the first PCR. This ensures that the quality of the DNA samples is preserved for the sequencing run







