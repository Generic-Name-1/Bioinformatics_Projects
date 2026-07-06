The purpose of this paper is to create a model to predict survival and patient treatment outcomes.

"The current study investigated putative genetic signatures associated with CRC aggressiveness. The GW identification based on RNA‐seq was used to identify genes driving tumorigenesis and progression, 
and then we examined whether these signatures could identify patients who would benefit from adjuvant chemotherapy." - Kim et al 2014


GSE Datasets:

1) GSE50760 is the dataset of 18 patients generated in a hospital in Korea which they used to help develop the model

2) **(HI cohort, GSE14297, n = 48)** was a validation set that was used to validate the model that they generated. 
  " In the HI cohort, PC and matched MC from the same patient were assayed by gene expression profiling in 18 pairs. 
  Additionally, expression data of NC and normal liver tissue exist in the dataset (Stange et al., 2010)."
  
3) To develop a risk score classifier for predicting CRC outcomes, data collected for the Cartes d'Identité des Tumeurs (CIT) program from the French Ligue Nationale Contre le Cancer was used as a development data set **(CIT cohort, GSE39582, n = 566)**.
In the CIT cohort, patients who received preoperative chemotherapy and/or radiation therapy and those with primary rectal cancer were excluded. 

3) To validate our classifier, we used a gene expression data set that was generated from fresh‐frozen tumour specimens retrieved from the tissue banks of the Royal Melbourne Hospital, Western Hospital, and Peter MacCallum Cancer Centre in Australia and 
the H. Lee Moffitt Cancer Centre in the USA **(AUS cohort, GSE14333, n = 229)**. In the AUS cohort, individuals who had received preoperative chemotherapy and/or radiotherapy or samples in which tumour‐derived total RNA was inadequate for microarray analysis [RNA integrity number (RIN) < 6] were excluded