# Transcriptomic Prediction for Zika Virus Susceptibility in Glioblastoma Using Feature Selection and Machine Learning Approaches

This project was developed with U.P. Oncolytics and presented at the 2026 AACR Special Conference: Brain Cancer

## Introduction
Glioblastoma (GBM) remains highly resistant to conventional therapies due to the blood-brain barrier, tumor heterogeneity, immunosuppression, and diffuse infiltration. Oncolytic virotherapy offers a promising strategy to overcome these barriers by selectively infecting tumor cells while stimulating anti-tumor immunity.

Zika virus (ZIKV) is a strong candidate for GBM oncolytic therapy due to its natural neurotropism and ability to infect neural progenitor-like cells present in GBM. While ZIKV enters cells through transmembrane receptors such as AXL, receptor expression alone is insufficient for productive infection.

To identity transcriptional features underlying ZIKV susceptibility, we analyzed RNA-seq data from 15 GBM cell lines (10 patient-derived, 5 commercial; 60 samples total).

<img width="765" height="447" alt="Screenshot 2026-04-07 at 9 02 13 AM" src="https://github.com/user-attachments/assets/2e9c95e3-cf64-4f00-b98c-8970d7c57c19" />

**Figure 1. Computational pipeline for identifying transcriptomic predictors of ZIKV susceptibility.**

RNA-seq data were processed through a multi-step computational pipeline including preprocessing, differential expression analysis, functional enrichment, feature selection, and machine learning classification. This workflow integrates biological interpretation with predictive modeling to identify gene signatures associated with Zika virus susceptibility. 

## Differential Expression
* Differential expression analysis identified large-scale transcriptomic differences between ZIKV-susceptible and resistant GBM cell lines. 
* Across 34,895 detected genes, we identified 3,162 significantly upregulated genes and 2,482 significantly downregulated genes (adjusted p-value < 0.05).
* Principal component analysis (PCA) reveals clear separation between susceptible and resistant cell lines, indicating that baseline transcriptomic difference strongly associate with viral susceptibility (Figure 2).

<img width="820" height="551" alt="Screenshot 2026-04-07 at 9 03 51 AM" src="https://github.com/user-attachments/assets/6f553839-d347-482c-aa7f-4a17d81a9303" />

**Figure 2. Transcriptomic variation separates resistant and susceptible glioblastoma cell lines.**

Principal component analysis (PCA) shows clear separation between resistant and susceptible cell lines, indicating that global transcriptional programs are strongly associated with ZIKV infection phenotype.

## Functional Analysis
Gene Set Enrichment Analysis (GSEA) in patient-derived cell lines identified 872 significantly enriched Gene Ontology (GO) biological processes (adjusted p-value < 0.05). 2 dominant biological themes emerged: 

**1. Antiviral and Immune Signaling**

Immune-related pathways including interferon signaling, inflammatory responses, and antiviral defense were enriched (245 GO terms), indicating that host immune response influences infection efficiency.

**2. Neural Development**

Pathways related to neurogenesis, gliogenesis, and neuronal differentiation (17 GO terms) were enriched, signifying that neural lineage programs increase ZIKV susceptibility, consistent with viral neurotropism.

<img width="819" height="488" alt="Screenshot 2026-04-07 at 9 05 39 AM" src="https://github.com/user-attachments/assets/e2ae4d21-6c49-4193-bad2-8661001a81a8" />

**Figure 3. Top GO terms: antiviral and immune pathways characterize resistance-associated transcriptional programs.**

Analysis of enriched GO terms reveals patterns of antiviral and immune signaling processes, suggesting that intrinsic antiviral responses may contribute to resistance to ZIKV infection.

## Feature Selection and Classification
**Feature Selection Strategies**
* Method 1: PCA (Unsupervised) – Top 20 genes contributing to PC1 and PC2 
* Method 2: PCA + Differential Expression (Supervised) – Intersection of top 50 genes from PC1-PC3, top 100 DEGs

**Random Forest Classifiers** (300 trees) were trained using each feature set
* Stratified cross-validation (Stratified-CV) 
* Leave-one-out cross-validation (LOO-CV)
* Leave-one-cell-line-out cross-validation (LOCO-CV)
* External validation (patient trained, public tested)

**Machine Learning Prediction**

Supervised, biologically-informed feature selection dramatically improves model generalizability. Although LOO-CV and Stratified-CV achieve perfect AUC values, these classification methods are prone to overfitting. LOCO-CV and external validation are not prone to overfitting and represent real-world scenarios by encountering new biology and are nevertheless able to accurately predict ZIKV susceptibility. (Figure 4)

<img width="812" height="405" alt="Screenshot 2026-04-07 at 9 06 40 AM" src="https://github.com/user-attachments/assets/29171060-1edf-4db8-b318-acc0b5a4ae6c" />

**Figure 4. Biologically informed feature selection improves strict classifier performance.**

Four Random Forest Classifiers were trained using two feature selection strategies. Classifiers trained using method 2, the combined PCA + differential expression feature set, achieved strong and consistent performance, suggesting that this approach captures biologically meaningful predictors that generalize to real-world data.

## Key Findings
Transcriptomic signatures accurately predict susceptibility to ZIKV infection.

* ZIKV susceptibility is associated with neural lineage transcriptional programs consistent with viral neurotropism.
* Antiviral and immune pathways contribute to heterogeneous infection responses.
* Biologically-informed feature selection combined with machine learning enables robust prediction across heterogeneous GBM models.
* These findings support the precision oncology framework development to identify GBM patients most likely to benefit from ZIKV-based oncolytic virotherapy.

## Future Direction
* Improving feature selection method: intersect current PCA + DEG gene set with top leading-edge genes from functional analysis to develop optimized biologically-informed gene-signature.
* Develop a minimally predictive gene signature (ideally < 10 genes) with strong performance (0.90 AUC or greater) necessary for clinical screening distribution.
* Validate predictive performance on independent GBM data.
* Test gene signature across other cancers, broadening ZIKV treatment applications.
