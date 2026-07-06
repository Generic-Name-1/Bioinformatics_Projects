



# Reproduction of Katase et al 2026

The purpose of this R Project is to reproduce [Katase et al 2026](https://www.cureus.com/articles/423507-differentially-expressed-genes-in-head-and-neck-squamous-cell-carcinoma-exploratory-research-using-the-cancer-genome-atlas-tcga-rna-sequence-data-and-deseq2-package#!) all
the figures as well as expand the analysis to look at different biological questions related to the same dataset.

# Goal of Katase et al 2026

Katase et al 2026 attempts to use R and the DESeq() package to perform exploratory research for Head and Neck Cancer from the TCGA-HNSC (The Cancer Genome Altas) to identify further 
understand how genetic change in Head and Neck cancers may occur compared to normal tissue and how these impacts may affect survival of patients suffering from Head and Neck Cancers. 
This is needed to identify new targets for either prognostic factors for cancer diagnosis or new therapeutic targets.

## Dataset

**Source:** TCGA-HNSC
- **Publication:** [Cureus, 2026](https://www.cureus.com/articles/423507-differentially-expressed-genes-in-head-and-neck-squamous-cell-carcinoma-exploratory-research-using-the-cancer-genome-atlas-tcga-rna-sequence-data-and-deseq2-package#!/
- **Samples:** 504 HNSC primary tumors + 44 adjacent head and neck cancer
- **Measurement:** Differential Gene Expression from RNA-SEQ data, Kaplan Meier Survival Curve analysis, Gene Set Enrichment Analysis, TPM expression

Note, during the downloading of the data, it was determined that there was some filtering. This is because there are 528 total cases, but 520 solid tumors with relevant RNA-seq data for analysis and 44 normal tissue compared to
504 solid tumors and 44 normal tissue reported in Katase et al 2026. They do not indicate, and it was unable to be identified, which criteria was used to exclude roughly 16 patients. Furthermore, a quick review
of the literature shows different studies use a different N of patients with solid head and neck tumors for RNA-Seq. Therefore, the result identified are similar, yet different in some ways from the results reported
in Katase et al 2026. However, it seems likely that the differences is due to the different number of patient samples.

Additionally, how they calculate their TPM values for certain figures is unclear as well. The tpm-unstranded counts from the TCGA-HNSC database was downloaded and used for relevant analysis using TPM counts, but it is unclear
from the Katase et al 2026 paper if those are the TPM values that they used for their analysis.Otherwise, the raw counts downloaded from the TCGA-HNSC database was used unless otherwise explained in the R Markdown files. Katase et al 2026 does not indicate how they obtained the TPM counts, so that is the other
likely cause for the difference in some of the results.


##File Naming Scheme

For the purpose of the File naming scheme, all figures and their associated files that reproduce a specific figure from Katase et al 2026 will have an associated Figure in the file name, such as Fig6a. If a file or figure
does not have that, it is not associated with any specific figure with respect to reproduction, but rather new analysis on this dataset.

##Figures

##

*Top_10_upregulated_Genes_KaplanMeier_Fig6a* -> Among the Top 10 upregulated genes as determined by differential gene expression where Log2FoldChange > 1 and sorted by padj and a Kaplan Meier curve was ran for each gene and correlated with Fig 6a.

*Top_10_downregulated_Genes_KaplanMeier_Fig6b* -> Among the Top 10 downregulated genes as determined by differential gene expression where Log2FoldChange < -1 and sorted by padj and a Kaplan Meier curve was ran for each gene and correlated with Fig 6b.

##

*DEG_Fig1* -> This figure is a volcano plot correlated to Figure 1 from Katase et al 2026 from the Differental Gene Expression (DGE) was performed to demonstrate upregulated and downregulated genes from the Differential Expression Analysis
of primary HNSC with normal tissue.

##

*Top_10_upregulated_Genes_by_pval_Fig5a* -> By sorting DGE results where where Log2FoldChange > 1 and sorted by padj and those genes were used to filter the TPM counts taken from the TCGA-HSNC and compared. It is known that TPM counts
are typically not the best metric to compare between many samples (Primary Tumor vs Normal Tissue), although that is what Katase et al 2026 did. An alternative metric is the use of variance stabilized counts which more appropriately
adjust for variances in the samples since we are not looking at gene expression between samples. This figure is correlated with Fig 5a.

*Top_10_upregulated_Genes_by_Log2FoldChange* -> By sorting DGE results where where Log2FoldChange > 1 and sorted by padj and those genes were used to filter the TPM counts taken from the TCGA-HSNC and compared. It is known that TPM counts
are typically not the best metric to compare between many samples (Primary Tumor vs Normal Tissue), although that is what Katase et al 2026 did. An alternative metric is the use of variance stabilized counts which more appropriately
adjust for variances in the samples since we are not looking at gene expression between samples.


###

*Top_10_downregulated_Genes_by_pval_Fig5b* -> By sorting DGE results where where Log2FoldChange < -1 and sorted by padj and those genes were used to filter the TPM counts taken from the TCGA-HSNC database and compared. It is known that TPM counts
are typically not the best metric to compare between many samples (Primary Tumor vs Normal Tissue), although that is what Katase et al 2026 did. This figure is correlated with Fig 5b.

*Top_10_downregulated_Genes_by_Log2FoldChange* -> By sorting DGE results where where pad < 0.05 and sorted by most downregulation of gene expression and those genes were used to filter the TPM counts taken from the TCGA-HSNC database and compared. It is known that TPM counts
are typically not the best metric to compare between many samples (Primary Tumor vs Normal Tissue).

###

*Top 10_genes_by_Survival_Difference_in_Months_padj_Table* -> A Table showing among the genes that were show to have a statistically significant difference in differential expression, which genes have the largest
difference in survival as determined by a Log Rank Test and Kaplan Meier Curve. The High and Low Expression is identified by indicating each sample as either above or below the mean(TPM) for that gene. Furthermore,
this table has the p-values adjusted using the Bonferroni-Hochberg correction to correct for multiple comparisons. Curiously, the gene *LINC0325* which is involved in immune modulation and killer T cells appears to have the 
greatest difference in overall survival. This is

###

Note: Again there are differences in the results, but it seems likely that the results are due to different sample sizes of initial tissues.

*ORA_GOBP_Fig3a* -> This Over Representation Analysis plot attempts to reproduce Fig 3a from Katase et al 2026 for upregulated genes, although there are some differences.

*ORA_GOCC_Fig3b* -> This Over Representation Analysis plot attempts to reproduce Fig 3b from Katase et al 2026 for upregulated genes, although there are some differences.

*ORA_GOMP_Fig3c* -> This Over Representation Analysis plot attempts to reproduce Fig 3c from Katase et al 2026 for upregulated genes, although there are some differences.

*ORA_KEGGLEGACY_Fig3c* -> This Over Representation analysis plot attempts to reproduce Fig 3d from Katase et al 2025 for upregulated genes, although

### The GSEA Analysis has not been performed yet or attempted to be reproduced




## KEY FINDINGS AND INSIGHTS and their comparison to Katase et al 2026

- Consistent with Katase et al 2026, genes like *CA9*, *MMP11*, and *IL11* were were among the top 10 upregulated genes in HNSC compared to normal tissue. In fact, this analysis showed the same top 10 upregulated genes when sorted by pval, while
for top 10 downregulated genes, there outlap with 7/10 genes overlaping, but there were a few genes such as *CST4*(encodes for protease inhibitor in salvia) and *CLEC3B* where were demonstrated to be the top 10 downregulated genes sorted by pvalue in this result, but not among Katase et al 2026. 
This does not mean they are not highly upregulated or downregulated respectively, but they were not in the top 10 when sorted by adjusted pvalue. Again, the differences between this analysis and Katase et al 2026 at this point is likely due to different number of patients due to 
unclear exclusion criteria, as well as unclear methodology for how TPM counts were calculated for later
downstream analysis.

- When sorting the Top 10 upregulated and downregulated genes strictly by log2FoldChange as long as the differential expression is statistically significant showed large overexpression of several genes not commonly expressed in normal 
tissues(*MAGEC2, MAGEB2, MAGEA1, MAGEA12*) and commonly overexpressed in melanoma that regulates promotion and gene expression. Furthermore, genes typically expressed in reproductive organs (*BRDT, NOBOX*) were substantially overexpressed in the HNSC tumors
compared to normal tissue. With respect to downregulation, there was large downregulation of several genes involved in salvia or salvia production(*STATH, HTN1, HTN3, SMRB3, BPIFA2, LACRT*) along with genes
like CST5.

- The overrepresentation analysis is similar, but has some differences compared to the overrepresentation analysis demonstrated in Katase et al 2026. This is likely due to the issues noted previously on determining which 
patients were excluded from their analysis. Furthermore, the ShinyGO software instructions were unable to reproduce the results.

- The PCA analyis shows that there is some difficulty separating the types of cells, indicating large genetic variety in the primary tumors compared to normal tissues, which could make it more difficult to differentiate differences
in expression of data.

- Survival analysis of the top 10 upregulated and downregulated genes as determined by sorting by adjusted p-values, a few of them have high and low expression demonstrating a statistically significant difference in survival.
This includes **NOSTRIN, IL23, and LINC01829** where Nostrin regulates nitric oxide synthase, IL23 which regulates an inflammatory response in the immune system as a pro-inflammatory cytokine, and LINC01829 which is a non-coding protein RNA.
These genes could be potential targets for treatments of Head and Neck Cancers.

- Survival analysis of the Top 10 genes with the largest difference in survival between high and low expression among genes that are statistically significant shows several genes of genes to target that could have
clinically relevant differences in survival. This includes **LINCO3025, TRBJ1-4, and ERFE** which encodes for specific long non-protein encoding RNA< T Cell Receptor Beta 1-4, erythroferrone respectively.
## Conclusion:

- Try to identify the exclusion criteria or look for exclusion criteria so that the number of patients with tumors matches N=504 rather than N=520
- Identify how they calculated or where they calculated TPM or where they downloaded the TPM Counts from
- Although not all the conclusion that were determined in this analysis matched the results of Katase et al 2026, the results were very close and much of the differences is probably due to the lack of detail
explaining how they excluded specific patients and what exact analysis was performed.
- As my first real attempt, I think I did a decent job trying to reproduce their work considering how little information, in my view, they give that allows us to reproduce their computational work. I can definitely come 
back and fix it up since I have my code and it is annotated.

## Tools used

**RStudio**

**R Version 4.5.2**

**Tidyverse 2.0.0** - Wickham H, Averick M, Bryan J, Chang W, McGowan LD, François R, Grolemund G, Hayes A, Henry L, Hester J, Kuhn M, Pedersen TL, Miller E, Bache SM, Müller K, Ooms J, Robinson D, Seidel DP,
  Spinu V, Takahashi K, Vaughan D, Wilke C, Woo K, Yutani H (2019). “Welcome to the tidyverse.” _Journal of Open Source Software_, *4*(43), 1686. doi:10.21105/joss.01686
  <https://doi.org/10.21105/joss.01686>.
  
**DESeq2 1.50.2 ** - Love, M.I., Huber, W., Anders, S. Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2 Genome Biology 15(12):550 (2014)

**survival 3.8.6 **

**survminer 0.5.2 **

**rstatix 0.7.3**

**TCGAbiolinks 2.38.0**

**SummarizedExperiment 1.40.0**

**ggpubr 0.6.3**

**annotables 0.2.0**

**biomaRt 2.66.2**
