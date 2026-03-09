# AML-venetoclax-response-AI-Capstone-2026

# AI Prediction of Venetoclax Response and Safety in Acute Myeloid Leukemia (AML)
Dr. Pratibha Choudhary (March 2026)

# Project Overview

Acute Myeloid Leukemia (AML) is an aggressive blood cancer with highly variable patient outcomes. Venetoclax (Venclexta), a targeted BCL-2 inhibitor developed by AbbVie, has improved treatment options for many AML patients, but not all individuals respond to therapy.
This project develops an AI-based predictive modeling framework that uses patient molecular data to estimate:
1.	Venetoclax treatment response (responder vs non-responder)
2.	Safety-related risk proxy derived from clinical AML risk stratification
The goal is to explore whether multi-omics molecular features can help predict treatment outcomes before therapy begins, supporting biomarker discovery and personalized medicine strategies.
________________________________________
# Dataset

This study uses the BeatAML2 harmonized dataset (Bottomly et al., 2022), one of the largest publicly available functional genomics resources for AML.
The dataset integrates multiple molecular modalities for AML patients:
•	RNA-seq gene expression
•	Whole-exome sequencing mutation calls
•	AML malignant cell-state programs
•	Clinical annotations
•	Ex-vivo Venetoclax drug sensitivity (AUC)
After preprocessing and feature integration, the modeling cohort included approximately:
•	382 AML patient samples for most analyses
•	309 samples for WGCNA module features
•	367 samples for pathway signature features
________________________________________
# Feature Engineering

To reduce dimensionality and improve biological interpretability, several transcriptomic feature representations were compared.
# 1. Gene-Level Representation
Genes200
A subset of 200 informative gene expression features combined with:
•	AML cell-state scores (6 programs)
•	Binary mutation panel (Mut50)

# 2. WGCNA Co-expression Modules
   
WGCNA_PC1(14)
Gene expression was summarized using 14 module eigengenes, representing coordinated transcriptional programs.
This approach reduces thousands of genes into a smaller set of biologically meaningful features.

# 3. Pathway / Signature Programs
   
Five biologically interpretable pathway scores were computed:
•	Monocytic differentiation
•	BCL2 / apoptosis signaling
•	Inflammatory signaling
•	Oxidative phosphorylation (OXPHOS)
•	Glycolysis

# 4. RF8 Literature Gene Panel
   
A compact 8-gene signature (RF8) proposed by Jin et al. (2025) was evaluated as a benchmark biomarker panel.
RF8 genes:
•	PDZK1IP1
•	AFAP1
•	MANEAL
•	SASH1
•	ROGDI
•	CEBPE
•	SLC9A3
•	PINK1
RF8 variants tested:
•	RF8 alone
•	RF8 + CellTypes
•	RF8 + Mut50
•	RF8 + CellTypes + Mut50
________________________________________

# Machine Learning Models

Logistic Regression (Baseline)
Logistic regression was used as the primary baseline model because it:
•	performs well on moderate-sized clinical datasets
•	is stable and interpretable
•	produces coefficients linked to biological hypotheses
________________________________________

# Multitask Neural Network

A two-head multitask neural network was implemented in PyTorch to jointly predict:
•	Venetoclax response
•	Safety proxy label
The architecture includes:
•	shared feature representation (shared layers)
•	two output heads (response and safety)
This design allows the model to learn shared biological signals between related tasks.
________________________________________

# Model Evaluation

All models were evaluated using:
5-fold stratified cross-validation
Metrics reported:
•	AUROC – ranking ability across thresholds
•	AUPRC – performance under class imbalance
________________________________________

# Key Results

Response Prediction Performance
Model	AUROC
Genes200 + CellTypes + Mut50	~0.86
WGCNA modules	~0.83
Pathway signatures	~0.84
RF8 + CellTypes	~0.86
Multitask Neural Network	~0.89
________________________________________

# Safety Proxy Prediction

Model	AUROC
Genes200 + CellTypes + Mut50	~0.82
WGCNA modules	~0.80
Signatures	~0.80
RF8 + CellTypes + Mut50	~0.80
Multitask Neural Network	~0.86
________________________________________

# Biological Insights

Model interpretation revealed important biological signals linked to Venetoclax response:
•	Monocytic differentiation programs associated with reduced drug response
•	Inflammatory signaling pathways
•	Metabolic programs (OXPHOS / glycolysis)

These findings align with prior AML studies linking cell differentiation state to Venetoclax resistance.
________________________________________

# Project Structure
project/
│
├── notebooks/
│   BeatAML2_pipeline.ipynb
│
├── data/
│   processed datasets
│
├── models/
│   logistic regression
│   multitask neural network
│
├── outputs/
│   figures
│   model results
│
└── README.md
________________________________________

# Example Visualizations

The project includes several model evaluation figures:
•	ROC curves for response prediction
•	ROC curves for safety prediction
•	Precision-recall curves
•	Model comparison plots
•	Mutation oncoprints
•	Feature importance analyses
________________________________________

# Potential Applications

This project demonstrates how multi-omics AI models may support:
•	treatment response prediction
•	biomarker discovery
•	clinical trial stratification
•	precision oncology decision support
________________________________________

# Technologies Used

•	Python
•	Pandas
•	Scikit-learn
•	PyTorch
•	Matplotlib / Seaborn
•	Jupyter Notebook
________________________________________

# References

Bottomly D. et al. (2022)
Integrative analysis of drug response and clinical outcome in AML.
Nature Cancer.

Jin et al. (2025)
RF8 gene panel for Venetoclax response prediction.
________________________________________

# Author

Dr. Pratibha Choudhary

Northwestern University

MS in Data Science (AI specialization)

Contact email -choudharypratibha.purdue@gmail.com
Linkedln- www.linkedin.com/in/pratibha-choudhary-ph-d-bio

