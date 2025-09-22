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


### How ChIP-seq Works: A Step-by-Step Workflow

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

### Statistical Methods 
🔹 1. Peak Calling (finding enriched regions)

***Goal***: Detect regions of the genome where read coverage is significantly higher than background.

***Statistical methods used***:

Poisson distribution (assumes reads fall randomly; early methods like MACS1).

Negative binomial models (handles overdispersion better, used in tools like DESeq2, edgeR, DiffBind).

Empirical background modeling with control/Input DNA.

***Tools***: MACS2, SICER, HOMER, Genrich.

***Multiple testing correction***: Benjamini–Hochberg FDR is commonly applied to peak p-values.

🔹 2. Differential Binding Analysis

***Goal***: Compare protein-DNA binding between conditions (e.g., wild type vs knockout).

***Statistical methods***:

Generalized linear models (GLMs) with negative binomial distribution → DESeq2, edgeR.

DiffBind (R package) → wraps these models for ChIP-seq data.

Outputs: log2 fold change, adjusted p-values (FDR).

🔹 3. Motif Enrichment Analysis

***Goal***: Identify DNA sequence motifs enriched in peaks (binding preferences of transcription factors).

***Statistical tests***:

Binomial test (observed vs expected motif occurrence).

Fisher’s exact test (peak sequences vs background sequences).

***Tools***: MEME suite, HOMER, FIMO.

🔹 4. Functional/Pathway Enrichment

***Goal***: Link peaks to nearby genes and test whether those genes are enriched in pathways.

***Statistical tests***:

Hypergeometric test / Fisher’s exact test (over-representation analysis).

Gene Set Enrichment Analysis (GSEA) for ranked gene lists.

***Tools***: GREAT, ChIPseeker, clusterProfiler.


### Sources: 

Shah, A. Chromatin immunoprecipitation sequencing (ChIP-Seq) on the SOLiD™ system. Nat Methods 6, ii–iii (2009). https://doi.org/10.1038/nmeth.f.247

Nakato R, Sakata T. Methods for ChIP-seq analysis: A practical workflow and advanced applications. Methods. 2021 Mar;187:44-53. doi: 10.1016/j.ymeth.2020.03.005. Epub 2020 Mar 30. PMID: 32240773.

Shah, A. Chromatin immunoprecipitation sequencing (ChIP-Seq) on the SOLiD™ system. Nat Methods 6, ii–iii (2009). https://doi.org/10.1038/nmeth.f.247


### Prompts

ChatGPT: Summarize briefly the mechanisms, applications and estimation methods of ChIP-Seq, cite your resources;

ChatGPT: write a short summary about the chip seq assay

