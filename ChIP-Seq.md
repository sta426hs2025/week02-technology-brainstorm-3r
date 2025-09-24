Group Members:

leah086

teodorako

natalijamojsilovic

## ChIP-Seq Summary
***Chromatin Immunoprecipitation*** followed by sequencing is an assay used to map protein–DNA interactions across the genome. The method combines immunoprecipitation of DNA fragments bound by a specific protein (such as a transcription factor or histone modification) with next-generation sequencing.
### Technology: 
Chromatin immunoprecipitation combined with high-throughput sequencing captures DNA fragments bound by transcription factors or modified histones.
### Application: 
This enables genome-wide mapping of protein–DNA interactions, identification of regulatory elements (promoters, enhancers), and comparison of binding landscapes between conditions (e.g., healthy vs. diseased tissue).
### Statistics: 
Computational analysis uses statistical models to distinguish true binding sites from background noise (Poisson/negative binomial models for peak calling, FDR correction for multiple testing, and GLMs for differential binding).

***What it does***:
Identifies where proteins bind to DNA.
Reveals the distribution of histone modifications that shape chromatin states.
***What it is used for***:
Studying gene regulation by mapping transcription factor binding sites.
Defining epigenetic landscapes, such as active promoters, enhancers, or repressed regions.
Comparing binding patterns between conditions (e.g., normal vs. disease).
Linking chromatin changes to development, cancer, and drug response

---

## How ChIP-seq Works: A Step-by-Step Workflow

The core principle is to cross-link proteins to DNA in vivo, immunoprecipitate the protein-of-interest along with its bound DNA fragments using a specific antibody, and then sequence those DNA fragments to pinpoint their genomic locations.

The ChIP-seq procedure can be broken down into several key steps, as illustrated in Fig.1. 
<div style="text-align: center;">
  <p><strong>Figure 1. ChIP-Seq wet-lab workflow overview.</strong></p>
</div>

![Fig.1 ChIP-Seq wet-lab workflow](https://media.springernature.com/full/springer-static/image/art%3A10.1038%2Fnmeth.f.247/MediaObjects/41592_2009_Article_BFnmethf247_Fig1_HTML.jpg?as=webp)
				

[1] ***Cross-linking***: Proteins are covalently fixed to DNA to preserve binding interactions.


[2] ***Chromatin isolation and shearing***: The DNA–protein complexes are extracted and fragmented into smaller pieces.


[3] ***Immunoprecipitation***: A protein-specific antibody selectively pulls down DNA fragments bound by the protein of interest.


[4] ***Cross-link reversal and protein digestion***: The DNA is released by reversing the cross-links and removing proteins.


[5] ***Library preparation***: Sequencing adaptors are ligated to DNA fragments, creating a library for high-throughput sequencing.

[6] ***High-throughput sequencing***

The DNA library is sequenced (typically on Illumina platforms), producing millions of short reads that correspond to the fragments originally bound by the protein of interest. 

[7] ***Downstream analysis***

***Motif discovery***: Identifying enriched DNA motifs in transcription factor peaks.

***Functional annotation***: Linking peaks to nearby genes or regulatory elements.

***Differential analysis***: Comparing binding between conditions (e.g., treated vs. control, WT vs. KO).

***Visualization***: Generating coverage tracks (bigWig) for genome browsers (IGV, UCSC).

---

 ## Statistical Methods - Downstream Analysis in ChIP-Seq

### 1. Motif Discovery
**Goal:** Identify enriched DNA motifs in transcription factor peaks.

ChIP-seq experiments generate millions of short DNA sequences (reads). When aligned to the genome, these reads form a coverage landscape. The aim is to detect regions where read density is statistically significantly enriched compared to random expectation.  

#### Statistical Modeling
- **Data type:** Count data (number of reads mapped to genomic regions)
- **Peak calling:** Sliding windows across the genome count reads in ChIP vs control samples.
- **Probabilistic models:** Determine if counts are unexpectedly high.

#### Methods:
- **Negative Binomial (NB) models**:  
  - Handle overdispersion better than Poisson.  
  - Used in tools like `DESeq2`, `edgeR`, `DiffBind`.  
  - NB introduces a **dispersion parameter** to account for variance beyond Poisson expectation.

- **Multiple testing correction:**  
  - **Benjamini–Hochberg FDR (False Discovery Rate)** applied to peak p-values.  
  - Prevents inflated false positives from millions of independent tests.

- **Functional annotation:** Link peaks to nearby genes or regulatory elements.



### 2. Differential Binding Analysis
**Goal:** Compare protein-DNA binding across conditions (e.g., treated vs. untreated, WT vs. KO).

- **Statistical method:** Generalized Linear Models (GLMs) with Negative Binomial error distribution.  
- **Tools:** `DESeq2`, `edgeR` (RNA-seq), `DiffBind` (ChIP-seq specific).

This identifies peaks where binding is **significantly increased or decreased** between conditions.



### 3. Motif Enrichment Analysis
**Goal:** Detect DNA sequence motifs enriched in peaks (transcription factor binding preferences).

- **Statistical tests:**
  - **Binomial test:** Compare observed vs expected motif occurrences.
  - **Fisher’s exact test:** Compare motif frequency in peak sequences vs background sequences.



### 4. Functional / Pathway Enrichment
**Goal:** Link peaks to nearby genes and test for pathway enrichment.

- **Statistical tests:**
  - **Hypergeometric test / Fisher’s exact test:** Over-representation analysis.  
  - **Gene Set Enrichment Analysis (GSEA):** For ranked gene lists.

---

## References
1. Shah, A. *Chromatin immunoprecipitation sequencing (ChIP-Seq) on the SOLiD™ system*. Nat Methods 6, ii–iii (2009). [DOI](https://doi.org/10.1038/nmeth.f.247)  
2. Nakato R, Sakata T. *Methods for ChIP-seq analysis: A practical workflow and advanced applications*. Methods. 2021 Mar;187:44-53. doi: 10.1016/j.ymeth.2020.03.005  
3. Zhang, Y., Liu, T., Meyer, C. A., et al. (2008). *Model-based Analysis of ChIP-Seq (MACS)*. Genome Biology, 9(9), R137.  
4. Benjamini, Y., & Hochberg, Y. (1995). *Controlling the False Discovery Rate: A Practical and Powerful Approach to Multiple Testing*. Journal of the Royal Statistical Society: Series B, 57(1), 289–300.



## Prompts 

ChatGPT: Summarize briefly the mechanisms, applications and estimation methods of ChIP-Seq, cite your resources


ChatGPT: write a short summary about the chip seq assay


DeepSeek: Computational analysis uses statistical models to distinguish true binding sites from background noise (Poisson/negative binomial models for peak calling, FDR correction for multiple testing, and GLMs for differential binding). Can you explain EXACTLY how these methods correlate to Chip seq, give examples and cite sources?


