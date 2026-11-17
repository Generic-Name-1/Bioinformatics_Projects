# Reproduction of Xiong et al 2020

The purpose of this R project is to reproduce as much as possible [Xiong et al 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC7467359/) to develop a model from The Cancer Genomic Atlas from the Lung adenocarcinoma (TCGA-LUAD) in that tries to predict
5 and 1 year survival rates as well as tumor growth, metastasis, and lymph node invasion risk.

# Goal of Xiong et al 2020

The goal of Xiong et al 2020 was to develop a gene-expression based model to predict certain clinical outcomes, such as risk of tumor growth, metastasis, or lymph nodes, or the 5 year and 1 year survival times.

# Datasets

**Source:** TCGA-LUAD
- **Publication:** [Xiong et al 2020](https://pmc.ncbi.nlm.nih.gov/articles/PMC7467359/)
- **Samples:** 518 Total Samples

In Xiong et al 2020, for the RNA-Sequencing analysis, they performed a 58 tumor samples that were matched with their patient equivalent of normal tissue. During the reproduction, although the code and criteria for the 58 tumor samples +
the normal matched sample was not provided, a criteria was developed to institute a 58 tumor sample dataset + the matching normal tissue, although it can not be 100% guaranteed that the samples are exactly the same. 
In order to obtain the 58 tumor samples + matched normal tissue, the data was grouped by each patient with their unique patient ID and all patients with at least 2 samples associated were kept. In this case, it meant that there was
at least 1 tumor sample and 1 normal tissue sample associated with that patient. Additionally, following criteria from the  [Broad Institute criteria](https://broadinstitute.atlassian.net/wiki/spaces/GDAC/pages/844334036/FAQ#FAQ-replicateFiltering) if you have multiple aliquot barcodes per sample,
we were able to exclude duplicate tumor samples and obtain a dataset where there are 58 tumor samples + an associated normal tissue matched for DESeq2 RNA-Seq.

For the survival analysis, 403 samples containing survival data was used including 371 total samples with complete data to do relevant TNM scoring. However, there was no code provided so it was impossible to determine how exactly
the criteria was determined. After the criteria was applied, only 322 samples were available with complete TNM data for scoring. This will be another factor on why the results will be different than the results reported by 
Xiong et al 2020.

**GSE43458**
- **Gene Expression Omnibus** [GSE43458](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE43458)
- **Samples:** Lung adenocarcinomas were comrpised of never-smoker (n=40) and smoker (n=40) adenocarcinomas. Normal lung tissue (n=30) were paired to 30 of the never-smoker cases.

**GSE32863**
- **Gene Expression Omnibus** [GSE32863](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE32863)
- **Samples:** 58 lung adenocarcinoma and 58 adjacent non-tumor lung fresh frozen tissues were macrodissected, and total RNA was isolated to be analyzed using the Illumina HumanWG-6 v3.0 expression beadchip.

**GSE10072**
-  **Gene Expression Omnibus** [GSE10072](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE10072)
- **Samples:** This report is based on 122 samples, of which 15 duplicates were averaged, resulting in 107 final expression values from 58 tumor and 49 non-tumor tissues from 20 never smokers, 26 former smokers, and 28 current smokers.

# Scripts

**TCGA_LUAD_Import.Rmd** --> This script imports the Lung adenocarcinoma dataset from the TCGA-LUAD dataset 

**TCGA_LUAD_DEG_Fig1D.Rmd** --> This script is where the Differential Gene Expression using DESeq2 is performed.

**GSE43458_Import.Rmd** --> This script imports the Lung adenocarcinoma dataset from the NCBI GEO GSE43458

**GSE43458_DEG.Rmd** --> This script is where the Differential Gene Expression using DESeq2 is performed.

**GSE32863_Import.Rmd** --> This script imports the Lung adenocarcinoma dataset from the NCBI GEO GSE32863

**GSE32863_DEG.Rmd** --> This script is where the Differential Gene Expression using DESeq2 is performed.

**GSE10072_Import.Rmd** --> This script imports the Lung adenocarcinoma dataset from the NCBI GEO GSE10072

**GSE10072_DEG.Rmd** -- This script is where the Differential Gene Expression using DESeq2 is performed.

**Identifying_Overlapped_DEG.Rmd** --> This script is where the genes that are differentially expressed in each of the 4 lung adenocarcinoma datasets was obtained.

**Cox_Proportional_Hazard_and_Survival_Curve.Rmd** --> This is the initial R script where the cox proportional hazard model for predicting the patient survival based on gene expression.
A new script was made where this was reproduced, but the code became cleaner and easier to read. For the purposes of transparency, this r markdown file was kept.

**Coxph_survival_curve_simplified_PFS.Rmd** --> This script is where the coxph model for predicting the PFS (Progression Free Survival) for the patients from the LUAD dataset

**Coxph_survival_curve.Simplified.Rmd** --> This script is where the coxph model for predicting the OS (Overall Survival) for the patients from the LUAD dataset

**Univariate_and_Multilogistic_Modeling.Rmd** --> In this R File, the univariate and multiple logistic modeling for Tumor Growth, Lymph Invasion, and
Metastasis is performed. It should be noted that the # of patients in this analysis is different than what was shown in Xiong et al 2020. They do not provide
any code to help in the patient selection process, and due to this, the figures are similar, yet different in some ways. Absolute 100% reproducibility was not able
to be obtained.

**Univariate_and_Multilogistic_Modeling_V2.Rmd** --> A duplicated version of the above file except with a different filtration criteria.
In this example, no figures were saved but the code from the analysis was kept.

**Univariate_and_Multilogistic_Modeling_V3.Rmd** --> A duplicated version of the above file except that all patient samples were included even if there was no full TNM scoring.
In this example, no figures were saved but the code from the analysis was kept.



#Figures

--Differential Gene Expression--

*DEG_TCGA-LUAD_1D.png* --> For the TCGA-LUAD Dataset using the 58 tumor samples + matched normal tissue, DESeq2 was used to perform differential expression analysis and this figure is the
differential gene expression from that analysis which is supposed to reproduce Fig 1D from Xiong et al 2020. It *should* be noted that the results do not exactly match, but this is likely due to 
lack of clarity of what exact steps were performed (since no code was provided) as well as no specific criteria on how the 58 samples were chosen. Additionally, a third possibility is due to using a later
version of R and a later version of DESeq and other packages

*PCA-TCGA-LUAD.png* --> Principle Component Analysis was performed and then a PCA plot was obtained using the MASS and Factoextra packages to show the distribution of the PCA plot
to look for any other causes for variation in the dataset that could distort later analysis.

*PCA-GSE43458.png* --> Principle Component Analysis was performed and then a PCA plot was obtained using the MASS and Factoextra packages to show the distribution of the PCA plot
to look for any other causes for variation in the dataset that could distort later analysis.

*PCA-GSE32863.png* --> Principle Component Analysis was performed and then a PCA plot was obtained using the MASS and Factoextra packages to show the distribution of the PCA plot
to look for any other causes for variation in the dataset that could distort later analysis.

*PCA-GSE10072.png* --> Principle Component Analysis was performed and then a PCA plot was obtained using the MASS and Factoextra packages to show the distribution of the PCA plot
to look for any other causes for variation in the dataset that could distort later analysis.

*DEG_GSE34358_Fig1B.png* --> For the GSE34358 dataset, the limma() package was used for the samples and differential gene expression was used using a simple contrast design to compare 
the results in LUAD tumor tissue compared to normal lung tissue.

*DEG_GSE32863_Fig1A.png* --> For the GSE32863 dataset, the limma() package was used for the samples and differential gene expression was used using a simple contrast design to compare 
the results in LUAD tumor tissue compared to normal lung tissue.

*DEG_GSE10072_Fig1C.png* ---> For the GSE10072 dataset, the limma() package was used for the samples and differential gene expression was used using a simple contrast design to compare 
the results in LUAD tumor tissue compared to normal lung tissue.

--Overrepresentation Analysis--

**Overreprsentation_Analysis_Combined_Fig2B.png** --> A figure showing the overrepresentation analysis of genes that were either upregulated or downregulated to a statistically significant
degree compared to normal tissue and the pathways associated with those genes that were enriched. An attempted replication of Figure 2B from Xiong et al 2020*

**Overrepresentation_Analysis_Upregulated.png** --> A figure associated with the over representation analysis of genes that were statistically significantly upregulated.

**Overrepresentation_Analysis_Downregulated.png** --> A figure associated with the over representation analysis of genes that were statistically significantly downregulated.

-- Tumor Growth Risk Logistic Modeling --

**Univariate_Model_TumorRiskModel_Fig3a.png** --> A Figure showing coeff of the effect of each gene with the statistical significant of each gene in the y axis for genes that impact risk of new tumor growth. 
Due to Xiong et al 2020 not running multiple comparisons, no multiple comparisons were run. This plot shows about 6 genes were shown to individually have a statistically significant impact on risk of new tumor growth. 
This figure is related to Figure 3a from Xiong et al 2020.

**TumorGrowthRisk_Genes_Univariate_Model.txt** --> A txt file of a list of all the genes that had a statistically significant impact on new tumor growth

**Multiple_Logistic_TumorGrowth_RiskLevel_ROC_Fig_3e.png** --> Figure that is the equivalent of Figure 3e from Xiong et al 2020. This figure shows the ROC
curve from the multiple logistic regression model with the AUC and other parameters showing how effective the logistic model is at identifying the risk for 
new tumor growth.

**Optimized_Multiple_Logistic_Model_TumorGrowthRisk_3D.png** --> This figure is equivalent to Figure 3D from Xiong et al 2020. In this figure, we get
the odds ratio and 95% CI interval for each gene as the expression of the gene increases on the log odds of the risk of tumor growth.

-- Lymph Node Invasion --

**Univariate_Model_LymphInvasionModel_Fig3b.png** --> A Figure showing coeff of the effect of each gene with the statistical significant of each gene in the y axis for genes that impact lymph node invasion. 
Due to Xiong et al 2020 not running multiple comparisons, no multiple comparisons were run. This plot shows about 14 genes were shown to individually have a statistically significant impact on risk of new lymph node invasion. 
This figure is related to Figure 3b from Xiong et al 2020.

**LymphGenes_Univariate_Model.txt** --> A txt file of a list of all the genes that had a statistically significant impact on lymph invasion

**Multiple_Logistic_Lymph_Invasion_ROC_Fig_3g.png** --> Figure that is the equivalent of Figure 3g from Xiong et al 2020. This figure shows the ROC
curve from the multiple logistic regression model with the AUC and other parameters showing how effective the logistic model is at identifying the 
risk of lymph node invasion.

**Optimized_Multiple_Logistic_Model_LymphInvasion_3F.png** --> This figure is equivalent to Figure 3F from Xiong et al 2020. In this figure, we get
the odds ratio and 95% CI interval for each gene as the expression of the gene increases on the log odds of the risk of lymph node invasion.

-- Metastasis Logistic Modeling --

**Univariate_Model_MetastasisModel_Fig3b.png** --> A Figure showing coeff of the effect of each gene with the statistical significant of each gene in the y axis for genes that impact metastasis. 
Due to Xiong et al 2020 not running multiple comparisons, no multiple comparisons were run. This plot shows about 3 genes were shown to individually have a statistically significant impact on metastasis. 
This figure is related to Figure 3c from Xiong et al 2020.

**MetastasisGenes_Univariate_Model.txt** --> A txt file of a list of all the genes that had a statistically significant impact on metastasis

**Multiple_Logistic_Metastasis_ROC_Fig_3i.png** --> Figure that is the equivalent of Figure 3g from Xiong et al 2020. This figure shows the ROC
curve from the multiple logistic regression model with the AUC and other parameters showing how effective the logistic model is at identifying the 
risk of metastasis.

**Optimized_Multiple_Logistic_Model_Metastasis_3H.png** --> This figure is equivalent to Figure 3H from Xiong et al 2020. In this figure, we get
the odds ratio and 95% CI interval for each gene as the expression of the gene increases on the log odds of the risk of metastasis.


--- Survival Analysis and Correlation Plots ---

**Statistically_Significant_Genes_On_Survival.png** --> After running multiple coxph curves for each covariate (gene), and we determined
which genes based on the coxph model had a statistically significant impact on patient survival. After the list of those genes were obtained,
a Kaplan Meier Survival curve + Log rank test was performed on each of those genes to see how high and low expression of those genes impacts
patient survival. *note: This is not using the kaplan meier survival curve to identify which genes had a statistically significant impact on 
patient surviva. Although that was performed in the Rmarkdown file, no figures were created. This takes the genes that were shown to have 
statistically significant impact on patient survival by the coxph model, and then a Kaplan Meier Curve + Log Rank test was performed*

**Figure_4a_Correlation_of_Genes_CoxPropHazards.png** --> Correlation plot demonstrating the correlation between expression of each of the genes
that had a statistically significant impact on patient survival. This is correlated approximately with Figure 4a from Xiong et al 2020, although it
should again me noted the results are not the same.

**Cox_Prop_Model_StepAdjusted_SurvivalCurve_Fig4D.png** --> Figure is correlated with 4D from Xiong et al 2020. This figure shows what the 5 year and 
1 year patient survival rates are from the *backwards selection* chosen coxph model.

**Coeffs_of_genes_of_OptimizedCoxPropModel_Fig4B.png** --> Figure is correlated with 4B from Xiong et al 2020. This figure demonstrates the coefficients
of the genes that are in the optimized coxph model where the dangerous factor increases the chance of death at higher expression, and the protective factor
will reduce it at higher expression.

**5_year_survival_plot_Predicted_vs_Actual_4G.png** --> This plot shows the optimized coxph model predicted survival rates compared to the actual rates around the 
5 year survival mark. This figure is correlated with Figure 4G from Xiong et al 2020

**1_year_survival_plot_Predicted_vs_Actual_4F.png** --> This plot shows the optimized coxph model predicted survival rates compared to the actual rates around the 
1 year survival mark. This figure is correlated with Figure 4F from Xiong et al 2020



--- Key Results and Conclusions ---

**Differential Gene Expression**

Dataset, # of Upregulated Genes, # Downregulated Genes, Xiong et al 2020 or the Reproduction

TCGA-LUAD, 6426 ,  4391  , Reproduction of Xiong et al 2020
TCGA-LUAD, 2976 ,  2183  , Xiong et al 2020

GSE10072, 172, 320 , Reproduction of Xiong et al 2020
GSE10072, 199, 405 , Xiong et al 2020

GSE32863, 368, 628, Reproduction of Xiong et al 2020
GSE32863, 492, 738, Xiong et al 2020

GSE43458, , 236 , 632, Reproduction of Xiong et al 2020
GSE43458, 223 , 611 , Xiong et al 2020

**There are 52 upregulated and 180 downregulated genes that are consistent among all 4 datasets in Xiong et al 2020, while in this reproduction
of Xiong et al 2020 there are 35 upregualted and 130 downregulated genes among all 4 datasets. The likely cause of the difference is due to the 
lack of code provuded which led to assumptions in the pre-processing steps and differential gene expression. Another potential cause is that the 
R version and packages of DESeq2 are different versions**

**Over representation Analysis**

- The Overrepresentation analysis using Clusterprofiler were similar in showing their respective pathways that were differentially expressed between normal and tumor tissues. 
Some examples that were over represented in both Xiong et al 2020 and this reproduction in R is differential expression with respect to genes
related to the extracellular matrix organization, extra cellular structural organization, and extracellular receptor interactions. This suggests that in 
LUAD (Lung Adenocarcinoma) cancers, one of the potential drivers of carcinogenesis is genetic changes in genes that regulate the extracellular matrix and 
inter cellular communication, although this is not the only driver with respect to genetic changes. There appears to be changes in expression in genes related
to radical oxygen species and Glucocorticoids responses, indicating a role in both ROS modulation and immune/inflammation responses in LUAD carcinogenesis.

**Tumor Growth Risk, Lymph Node Invasion, and Metastasis Risk model**

Compared to Xiong et al 2020, the logistic regression models predicting tumor growth risk (3e), lymph node invasion risk (3g), and risk of metastasis (3i) have similar predictive 
power with respect to the the AUC of the ROC curve. Where in Xiong et al 2020, the models had an AUC of 0.74, 0.687, and 0.823 for tumor growth risk, lymph node invasion risk, and risk of 
metastasis respectively. This is compared to the AUC in the logistic models calculated in the reproduced figures showing an AUC of 0.7, 0.68, and 0.72 respectively; this demonstrates that
the reproduced models showed similar predictive power compared to the models shown in Xiong et al 2020. This is in spite of the fact that the genes that were included in the model, by the 
use of backwards selection, were not exactly the same. *This is likely the case for similar reasons as indicated in other secitons in that code was not provided, so certain specific
parameters on how the data was analyzed could not be obtained and assumptiosn were made. Additionally, the fact that previous steps had different results due to unclear code and different
results likely lead to downstream changes even further compared to Xiong et al 2020. Finally, the fact that the R packages used are different versions could be a 3rd contributing factor.*

For example, included in the model for predicting tumor risk in Xiong et al 2020, the genes are CAV1, GPC3, LDLR, and LIMCH1; this is contrasted to the model identified in the reproduction
which included the genes TIMP1, IL7R, and GPC3. GPC3, which is included as a significant factor in predicting risk of tumor growth in both Xiong et al 2020 and the reproduction, is a gene
that [regulates cell division and growth and is located on the cell surface](https://www.ncbi.nlm.nih.gov/gene?Db=gene&Cmd=ShowDetailView&TermToSearch=2719). This is consistent with the 
overrepresentation analysis which indicated that changes in expression of genes related to the ECM or cellular membrane are differentially expressed between healthy and malignant cells in
LUAD.

With respect to modeling the risk of lymph node invasion, Xiong et al 2020 optimized model included CYP4B1, EMP1, GPRC5A, NDNF, SMAD6 compared to SLC7A5, PAPSS2, CDH3, CBX7, C4BPA.

With respect to modeling risk of metastasis, Xiong et al 2020 reported an optimized model included CD36, HEY1, HOXA5, LIMCH1, TBX3, and TYMS compared to ECT2 and LCMD1.


**Survival Analysis**

After developing a multilogistic model for determining the risk of tumor growth, lymph node invasion, and risk of metastasis, a cox proportional model was developed to predict both
overall survival (OS) and PFS (Progression Free Survival) for patients based on gene expression. After running a repeated log rank test with associated Kaplan Meier Survival Curve and
adjusted for multiple comparisons, 12 genes were shown to have a statistically significant impact compared to 49 genes identified by Xiong et al 2020. Through the use of backwards selection, 
to be consistent with Xiong et al 2020, 5 genes were left in the cox proportional hazard model to predict overall patient survival. These genes were TOP2A, IL7R, TCN1, KLF4 and TPX2 compared to 
SLC2A1, GOLM1, ASPM, TOP2A, TYMS, CA4, MFAP4, HOXA5, EMCN, FBLN5 in the optimized cox proportional hazard model in Xiong et al 2020. Consistent with both models is the gene TOP2A, 
or DNA Topoisomerase II Alpha, which regulates transcript and replication, was found to be important in predicting overall patient survival. 

IL7R - [Interleukin-7 receptor subunit alpha](https://www.genecards.org/card/IL7R?search=IL7R) binds to IL7 and regulates lymphocyte activity as well as controlling cell signaling.
TOP2A - [DNA Topoisomerase ll Alpha](https://www.genecards.org/card/TOP2A?search=TOP2A) controls DNA replication by regulating the splicing and breaking of duplex DNA
TCN1 - [Transcobalamin 1](https://www.genecards.org/card/TCN1) regulates the import of cobalamin into the cell in the extracellular region
KLF4 - [zinc finger transcription factor](https://www.genecards.org/card/KLF4?search=KLF4) which regulates DNA transcription and plays a role in gene expression and the cell cycle
TPX2 - [TPX2 Microtubule Nucleation Factor](https://www.genecards.org/card/TPX2?search=TPX2) which regulates microtubule formation during mitotic development and plays a role in the cell cycle and 
cell division.

SLC2A1 - [GLUT1, a facilitative glucose transporter](https://www.genecards.org/card/SLC2A1?search=SLC2A1) mediates glucose and other sugar import/export into the cell and consequently plays a role
in cellular energy and biosynthesis.
GOLM1 - [Golgi Membrane Protein 1](https://www.genecards.org/card/GOLM1?search=GOLM1) regulates protein synthesis and expression in the rough ER.
ASPM - [Assembly Factor For Spindle Microtubules](https://www.genecards.org/card/ASPM?search=ASPM) regulates microtubule and spindle formation during cell division
TYMS - [thymidylate synthase](https://www.genecards.org/card/TYMS?search=TYMS) is an enzyme that promotes the synthesis of dTMP that supports DNA repair and replication
CA4 - [Carbonic Anhydrase 4](https://www.genecards.org/card/CA4?search=CA4) reverses the hydration of carbon dioxide to bicarbonate.
MFAP4 - [Microfibril Associated Protein 4](https://www.genecards.org/card/MFAP4?search=MFAP4) helps maintain the structure of the ECM and helps mediate cellular communication and forms the 
extracellular structure.
HOXA5 - [homeobox transcription factor 5](https://www.genecards.org/card/HOXA5?search=HOXA5) is a gene that regulates gene expression by acting on DNA polymerase 2 as a transcription factor.
EMCN -[endomucin](https://www.genecards.org/card/EMCN?search=EMCN) is a gene in the ECM that helps to regulate focal adhesion with other cells by inhibiting focal adhesion complexes.
FBLN5 - [fibulin-5](https://www.genecards.org/card/FBLN5?search=FBLN5) is a calcium binding ECM protein that regulates and supports elastic fiber assembly


The genes that were shown demonstrates in both models, the importance of genes related in DNA replication, repair, and the cell cycle in promoting carcinogenesis and their ability to be strong
prognostic indicators for patient survival. Additionally, these models were consistent with the over representation analysis showing that genes related to the ECM or DNA repair/transcription which
were overrepresented in differential expression also are important

With respect to Disease Free Survival or Progression Free Survival (PFS), after running repeated univariate log-rank tests and controlling for multiple comparisons, there are no genes
that have a statistically significant difference, unlike what Xiong et al 2020 demonstrated. Due to this, there is no cox proportional model for predicting PFS due to no genes having a 
statistically significant impact on patient PFS.



-- Final Conclusions --

In conclusion, this attempted reproduction of Xiong et al 2020 in 2026 show broad agreement with the conclusions of Xiong et al 2020, even if the exact results diverged in some areas and exact results
were not able to be reproduced. In Lung Adenocarcinoma, genes related to DNA repair and transcription as well as genes related to intercellular communication and the extracellular matrix ECM seem to play
important roles in the development of Adenocarcinoma. This is consistent with other studies and reviews demonstrating the importance of the [ECM](https://pmc.ncbi.nlm.nih.gov/articles/PMC7516130/) and
in lung adenocarcinoma.

Some likely causes for the discrepancies between Xiong et al 2020 and the results of the reproduction are a couple factors. One factor is that no code was provided in Xiong et al 2020, so exact parameters
and data processing is not known, and assumptions were made during the data processing and analysis steps. Additionally, as the initial DEG and data processing early on was likely slightly different, those 
differences were compounded downstream so that downstream analysis is likely more divergent than early data processing and analysis. Finally, another factor is that the R version and package versions were older
in 2020 compared to 2026, and in fact using those old package versions was unable to be done.

-- Other Important Info ---

R Version 4.5.2
