---
editor_options: 
  markdown: 
    wrap: 150
---

# Reproduction of Zhu et al 2018

The purpose of this R Project is to reproduce [Zhu et al 2018](https://www.spandidos-publications.com/10.3892/mco.2018.1728) and to demonstrate that
the overall results as demonstrated in Zhu et al 2018 can be reproduced.

##Differences with Zhu et al 2018## 

As noted later on, the overall results have been reproduced, although there are some differences between the
analysis shown here and the results demonstrated in Zhu et al 2018. One factor is that the lack of clarity of the methods meant that some assumptions
had to be made which may not be true to what was performed in 2018. Additionally, R version 3.5.1 used in Zhu et al 2018 is very out of date and the computer used was unable
to run the old version. Additionally, Zhu et al 2018 used GraphPad Prism for certain analysises, but all analysis done here was performed in R and required the use of
packages that may have not been used in this analysis. Due to these differing factors, there are some differences between what Zhu et al 2018 reported
and the results of this attempted reproduction, although the overall analysis is consistent with the results they demonstrated.

#Goal of Zhu et al 2018#

The goal of Zhu et al 2018 is to use the TCGA (The Cancer Genome Atlas) dataset and the Gene Omnibus Database (GSE14520) to do bioinformatic and
genomic analysis to identify potential targets for Hepatocellular Carcinoma (HCC), although it should be noted that the relevant naming for the TCGA
database is [TCGA-LIHC](https://portal.gdc.cancer.gov/projects/TCGA-LIHC). THey will use this information to potentially identify new potential
targets for future treatments and further understand the genetic differences between HCC cancers and their non-malignant counterparts.

##Datasets/Source Information##

**TCGA-LIHC** - **Publication:** [Zhu et al 2018](https://www.spandidos-publications.com/10.3892/mco.2018.1728) - 
**Samples:** 504 HCC primary
tumors + 55 non-tumor samples from the [TCGA-LIHC](https://portal.gdc.cancer.gov/projects/TCGA-LIHC) Database - 
**Measurement:** 
- RNA-SEQ with relevant PCA checks for potential batch effects. This pipeline does not start with the FASTQ files, but rather the Raw Counts from the TCGA database.
- Gene Enrichment Analysis
- Kaplan Meier Survival Curves
- Waterfall Plot
- Pearson Correlation Plots with CDK1 (A gene found to be important due to PPI Analysis which was not performed)
- Expression of CDK1 
- PPI Analysis


**GSE 14520** 
- **Publication:** [Zhu et al 2018](https://www.spandidos-publications.com/10.3892/mco.2018.1728) 
- **Samples** Gene expression data of human hepatocellular carcinoma (HCC) from [GSE14520](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=gse14520)

**Measurement**
- Batch Effect Correction (Due to different affymatrix uses) after importing the microarray counts
- Pearson Correlation Plots with CDK1 (A gene found to be important due to PPI Analysis which was not performed). CDC2 is another name for CDK1
- Expression of CDK1/CDC2 
- Kaplan Meier Survival Curves


#Results and Comparison with Zhu et al 2018

- After importing the raw RNA-SEQ counts from TCGA-LIHC and the Microarray data for the GEO GSE14520, relevant batch correction was performed and RNA-SEQ was performed for the
TCGA-LIHC data. The results demonstrated here were similar, but not exactly. This is potentially due to older versions of edgeR and RStudio used as well as Zhu et al using 
certain exclusion criteria that was unable to be exactly performed due to lack of clarity in the paper.

- The reproduction reported an upregulation of 644 genes and a downregulation of 135 that was statistically significant compared to 444 upregulation genes and 144 downregulated 
genes reported in Zhu et al 2018. The figure "DEG_Fig1.png" can be compared to Figure 1 in Zhu et al 2018 for comparison

- The Over Representation Analysis was performed in R in this reproduction compared to DAVID  in the study, and there are some differences between the two. DAVID was originally
going to be used, but it could not be found to work (I couldn't get it to work for some reason) via the online portal. Therefore, I decided to use the an R Package. For example, there was 
overlap in GOBP (Gene Ontology Biological Processes), there processes upregulated related to cell phase transition and the cell cycle, but the results reproduced here showed those pathways as well 
as pathways related to DNA repair being up regulated. With respect to Cellular Components, there are overlap in areas related to the centromere and the chromosome.
With respect to Molecular function, there is similarity because the DAVID showed upregulation of pathways connected microtubule binding and motor activity, and that is consistent with the reproduction 
which showed upregulation of pathways connected to microtubule and tubulin binding. However, the reproduction showed more upregulation of pathways related to ATP hydrolysis. This is important because it shows how the tumors
may be dependent on pathways that require lots of energy to maintain growth and repair DNA compared to normal tissues. With respect to KEGG (Kyoto Encyclopedia of Genes and Genomes), both Zhu et al 2018 and the 
reproduction showed upregulation of pathways related to the cell cycle, although our analysis showed upregulation of other pathways as well. This may likely be due to different names and annotation sets used by DAVID 
and the enricher function used in R to perform this type of analysis as well as the differentially expressed results having some differences (based on the DEG plot) compared to Zhu et al 2018. For the KEGG pathway, the KEGG Legacy
annotation set was used as that is likely the closest to the KEGG set that would have been used in 2018.

- PPI analysis was performed, but again due to the stringdbr portal used being updated and using version 9.0 vs 12.0 here (and being unable to revert to the old version) rather than being performed in R in this reproduction. Furthermore,
the results are likely different due to again the original differential expression analysis not being exactly the same, although there are strong similarities between the DEG results reported here and in Zhu et al 2018. However, slightly 
different versions of R, using GraphPad prism for certain analysises, as well as not clear exclusion criteria for patients made exact replication difficult. However, the results of the PPI (Protein-Protein Interaction) is shown

- From their PPI analysis, they chose CDK1 as a integral gene for further analysis. Although the PPI analysis reproduced in R did not show CDK1 as one of the Top 10 hub genes (indicated by # of connections), the later analysis was 
performed to try to reproduce their analysis. In this case, for both the TCGA-LIHC dataset from The Cancer Atlas Genome, as well as the Micro array data from GSE14520, were consistent with the figures shown in Zhu et al 2018
showing greater expression in the TCGA-LIHC set, both in paired samples and all the samples, as well as the Microarray data from the the GEO Omnibus.

- The Pearson Correlation analysis performed between CDK1 with the 9 other hub genes that they reported is consistent with the reproduction showing a positive correlation with 8 out of the 9 genes, with only a negative correlation with
FOS. As both CDK1 (a cell cycle regulator) and FOS (a protein involved in the formation on of AP-1) which regulates cell growth and cycle. In our case and in Zhu et al 2018, there was a strong negative correlation between expression 
of CDK1 and FOS. Interestingly, FOS expression has been shown to be associated with [apopotic cell death](https://www.ncbi.nlm.nih.gov/gene/2353). Perhaps, as the tumors enhance CDK1 which helps regulate the cell cycle, the tumor cells
are becoming more resistant to apoptotic cell death which is a major mechanism of cell death and target for cancer treatments along with ferroptosis, necrosis, and more.

- The Waterfall plot in Zhu et al 2018 is consistent with the reproduction here showing that in 49/50 paired samples, the expression of CDK1 is greater in the primary tumor compared to the normal tissue.

- Finally, Kaplan Meier plots were demonstrated to show how CDK1 expression may affect patient survival. Consistent with what Zhu et al 2018 showed, low expression of CDK1 is correlated with longer survival times. This implicates CDK1
as a factor that likely increases tumor aggressiveness and resistance to treatment which impact patient survival. Consequently, CDK1 is a potential target for future treatments which is what Zhu et al 2018 proposed as well. Our results
were consistent with both the TCGA-LIHC and GEO GSE14520 datasets in showing that a low CDK1 expression is a positive factor for patient survival compared to high expression.

#Conclusion:

Overall, our results from this reproduction were consistent with the data and conclusions from Zhu et al 2018. Due to factors such as different versions of R (that could not be reproduced that far back), use of GraphPad Prism in Zhu et al 2018, 
and the fact that certain inclusion/exclusion criteria for patients was not clear, and a different GO and PPI set, the results were not exactly the same as Zhu et al 2018. However, our results were consistent in terms of the Differential Gene Expression Plots
as well as showing the correlation between CDK1 and the 9 other hub gnees, even though our analysis failed to show the same Top 10 hub genes. Furthermore, our analysises both showed expression of CDK1 was higher in the tumor compared to non-tumor in 49/50 paired 
patient samples and that high expression of CDK1 is correlated with worse survival outcomes.

#Figures

##CDK1 Expression Comparison

**CDK1_Expression_Full_TCGA_set_Fig7b.png** --> Compares Expression in Log(CPM + 1) between tumor and non-tumor LIHC cancer in the entire TCGA-LIHC dataset and is associated with a reproduction of
Figure 7b.
**CDK1_Expression_GEO_GSE14529.png** --> Compares Expression in Log(CPM + 1) between tumor and non-tumor LIHC cancer in the entire GEO GSE14520 dataset and is associated with a reproduction of
Figure 7c.
**CDK1_Expression_Paired_Set_Fig7a.png** --> Compares Expression in Log(CPM + 1) between tumor and non-tumor LIHC cancer in the samples of paired TCGA-LIHC samples where there is 1 tumor
and 1 non-tumor sample per patient and associated with a reproduction of FIgure 7a.

## Differential Expression and Waterfall Plot

**CDK1-Waterfall_Plot_Fig8** --> Associated with reproduction of Figure 8 showing that 49/50 of the paired samples in the TCGA-LIHC dataset had greater expression in the tumor.

**DEG_Fig1.png** --> Associated with Figure 1 and is a reproduction of the Differential Expression Analysis using edgeR.

## PCA and LDA

**Normal_vs_Tissue_LDA.png** --> Linear Discriminant Analysis performed on the data from the TCGA-LIHC to look for any batch affects or anything that needs to be accounted for.

**Normal_vs_Tissue_PCA.png** --> Principle Component Analysis performed on the data from the TCGA-LIHC to look for any batch affects or anything that needs to be accounted for.

## Over Representation Analysis downregulation

**Over_Representation_downregulated_BP_Fig4a** --> GOBP analysis in R that is associated with a reproduction of figure 4a. The results have some similarities, but some differences.

**Over_Representation_downregulated_CC_Fig4b** --> GOCC analysis in R that is associated with a reproduction of figure 4b. The results have some similarities, but some differences.

**Over_Representation_downregulated_KEGG_LEGACY_Fig4d** --> GO KEGG LEGACY analysis in R that is associated with a reproduction of figure 4d. The results have some similarities, but some differences.

**Over_Representation_downregulated_MF_Fig4c** --> GOBP analysis in R that is associated with a reproduction of figure 4c. The results have some similarities, but some differences.

## Over Representation Analysis upregulation

**Over_Representation_upregulated_BP_Fig3a** --> GOBP analysis in R that is associated with a reproduction of figure 3a. The results have some similarities, but some differences.

**Over_Representation_upregulated_CC_Fig3b** --> GOCC analysis in R that is associated with a reproduction of figure 3b. The results have some similarities, but some differences.

**Over_Representation_upregulated_KEGG_LEGACY_Fig3d** --> GO KEGG LEGACY analysis in R that is associated with a reproduction of figure 3d. The results have some similarities, but some differences.

**Over_Representation_upregulated_MF_Fig4c** --> GOBP analysis in R that is associated with a reproduction of figure 4c. The results have some similarities, but some differences.

## PCA BIPLOT FOR MICROARRAY TO DEAL WITH BATCH EFFECTS 

**PCA_BIPLOT_MICROARRAY_AFFYMATRIX_BATCHCORRECTED.png** --> Corrected for batch affects from different affy matrix and the PCA plot was redone. Facets the samples by affymatrix type.

**PCA_BIPLOT_MICROARRAY_AFFYMATRIX.png** --> Prior to batch affect correction from different affy matrix and the PCA plot was redone. Facets the samples by affymatrix type.

**PCA_BIPLOT_MICROARRAY_TUMORTYPE_BATCHCORRECTED.png** --> Corrected for batch affects from different affy matrix and the PCA plot was redone. Facets the samples by Tumor Type type.

**PCA_BIPLOT_MICROARRAY_TUMORTYPE.png** --> Prior to batch affect correction from different affy matrix and the PCA plot was redone. Facets the samples by Tumor Type type.

## Pearson COrrelation

**PearsonCorrelation_Genes_Fig9.png** --> Associated with Figure 9, this shows the correlation between CDK1 and the 9 other hub genes.

## Kaplan Meier

**GEO_GSE14520_CDK1_Kaplan_Meier_10b** --> Associated with Figure 10b, a Kaplan Meier survival curve between high and low expression of CDK1 from the GSE14520 dataset.


**TCGA-LIHC_CDK1_Kaplan_Meier_10a.png** --> Associated with FIgure 10a, a Kaplan Meier survival curve between high and low expression of CDK1 from the TCGA-LIHC dataset.


#R Version and Tools#

- R 4.5.2
- The relevant packages and their versions should be in the renv.lockfile. In order to reproduce this analysis here, when R is loaded up in R version 4.5.2,
renv::restore should be used to restore the exact package versions for the packages that were used in this analysis.