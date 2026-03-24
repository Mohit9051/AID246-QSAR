# AID246-QSAR
Dose-aware QSAR model for predicting in vivo anticancer activity in the P1081 Chloroleukemia murine tumour model (PubChem AID 246) using multi-dose featurisation, group-aware cross-validation, and SHAP explainability


# Dose-Aware QSAR for In Vivo Anticancer Activity Prediction

This project presents a **dose-aware quantitative structure–activity relationship (QSAR) model** for predicting **in vivo anticancer activity** in the **P1081 Chloroleukemia murine tumour model** from **PubChem BioAssay AID 246**. The study uses multi-dose assay records, compound-level group-aware validation, and model interpretation with SHAP to build a reproducible machine-learning baseline for NCI Developmental Therapeutics Program data.

## Overview

Unlike standard in vitro QSAR workflows, this project models **in vivo antileukaemic activity**, where pharmacological effects depend not only on molecular structure but also on **dose**, absorption, metabolism, and whole-organism response. The dataset contains **152 unique compounds**, measured across **multiple dose levels**, producing **1,844 assay rows** with a strong class imbalance between active and inactive entries.

To preserve biological realism, dose is treated as a **feature** rather than a nuisance variable. The final feature set combines:

- Morgan fingerprints
- MACCS keys
- Physicochemical descriptors
- Log-transformed dose

## Key Highlights

- Dose-aware featurisation for multi-dose bioassay records
- Compound-level group-aware cross-validation to prevent leakage
- Comparison of multiple classifiers under class imbalance
- Random Forest selected as the strongest overall model
- SHAP-based interpretability to identify influential descriptors
- Designed for in vivo anticancer screening data from NCI DTP / PubChem AID 246 

## Dataset

The dataset is derived from the **P1081 Chloroleukemia** assay in PubChem AID 246.  
Each compound appears at multiple doses, and the endpoint is based on **T/C% survival ratio** in the murine model. Entries labelled active correspond to compounds with **T/C% ≥ 150**, while toxic entries are biologically distinct from simply inactive compounds.

## Methodology

The workflow includes:

1. Data cleaning and assay parsing  
2. Dose transformation and feature engineering  
3. Molecular descriptor generation  
4. Compound-level grouped train/test splitting  
5. Model training and evaluation  
6. SHAP interpretation of predictions :contentReference[oaicite:6]{index=6}

## Results

The best-performing model in the study was **Random Forest**, achieving:

- **ROC-AUC:** 0.674 ± 0.091
- **F1 score:** 0.361
- **MCC:** 0.182
- **Active recall on held-out test set:** 0.841
- **Hit-rate enrichment:** 1.88× over unranked selection :contentReference[oaicite:7]{index=7}

These results suggest that dose-aware modelling can reduce experimental workload while retaining most genuine active compounds.

## Biological Interpretation

SHAP analysis showed that **log-transformed dose** was the most influential predictor. Several MACCS features were also consistent with known anticancer pharmacophores, including patterns linked to:

- methotrexate-like amino/heterocyclic motifs
- vincristine-like ring nitrogen scaffolds
- cyclophosphamide-like chlorine-containing alkylating groups :contentReference[oaicite:8]{index=8}

## Why This Project Matters

This work helps recover value from historical NCI in vivo screening data and provides a reproducible framework for modelling other multi-dose bioassays. The approach is especially useful for prioritising compounds before expensive animal testing and for supporting oncology lead discovery efforts.

## Repository Contents

- `data/` — raw or processed assay data
- `notebooks/` — exploratory analysis and modelling notebooks
- `src/` — reusable code for preprocessing and training
- `models/` — saved trained models
- `results/` — evaluation outputs and plots

