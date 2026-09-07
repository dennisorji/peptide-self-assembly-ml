# Condition-Aware Machine Learning for Short-Peptide Self-Assembly

A leakage-aware machine-learning study of **short-peptide bulk state and supramolecular morphology** using peptide chemistry together with experimental conditions.

The central premise is that self-assembly is not a fixed property of peptide identity alone. A more realistic formulation is:

\[
Y = f(\text{peptide chemistry},\ \text{experimental environment})
\]

This repository accompanies **Paper 2** of my materials-informatics research portfolio and contains the full end-to-end analysis in one reproducible notebook.

## Why this project matters

Self-assembly databases contain repeated condition-level observations for the same molecular systems. A conventional random row split can therefore place the same peptide identity in both training and test data, giving an overly optimistic view of generalization.

This project addresses that problem by combining:

- publication- and provenance-aware data curation;
- chemically meaningful molecular-identity reconstruction;
- peptide physicochemical descriptors and experimental-condition features;
- molecular-identity-grouped model development;
- permanently sealed **unseen-molecule holdouts**;
- publication-aware robustness checks;
- molecule-cluster bootstrap confidence intervals;
- error analysis and feature-block sensitivity experiments.

## Key results

| Prediction task | Independent holdout | Selected model | Main performance |
|---|---:|---|---|
| Hydrogel vs non-gel | 115 rows, **20 unseen molecules** | Random Forest | ROC-AUC **0.977**, PR-AUC **0.882**, balanced accuracy **0.945**, MCC **0.836** |
| Non-gel vs hydrogel vs organogel | 129 rows, **20 unseen molecules** | Histogram Gradient Boosting | Macro ROC-AUC **0.783**, macro PR-AUC **0.555**, balanced accuracy **0.613** |
| Broad morphology | 59 rows, **14 unseen molecules** | Extra Trees | Macro ROC-AUC **0.980**, macro PR-AUC **0.925**, balanced accuracy **0.711**, MCC **0.665** |

The strong binary result should be interpreted together with the limited number of independent holdout molecules and the molecule-cluster confidence intervals reported in the notebook.

## 1. Why random row splitting is misleading

![Molecular leakage under random row splitting](figures/figure_1_random_split_leakage.png)

Approximately **87.3% of nominal test molecular identities** in a conventional random split were already present in training, while approximately **94.2% of test rows** came from molecular identities represented in training. This motivated molecule-grouped validation for the main claims.

## 2. Generalization to unseen molecules

![Binary hydrogel ROC curve](figures/figure_2_binary_holdout_roc.png)

The primary hydrogel/non-gel model was selected and tuned using development data only, then evaluated once on a permanent holdout containing 20 molecular identities absent from training.

## 3. Experimental environment matters

![Feature-block permutation importance](figures/figure_3_feature_block_importance.png)

Solvent identity and composition provide the strongest transferable feature block. However, fully aqueous analyses show that concentration, pH, temperature and other non-solvent conditions retain predictive information even after solvent-composition variation is removed.

## 4. Row count is not independent chemical sample size

![Independent support for broad morphology classes](figures/figure_6_broad_morphology_support.png)

Morphology auditing exposed a key limitation of condition-level databases: many rows may originate from very few independent molecular systems. For example, the crystalline class contained 34 observations but only **one molecular identity and one publication**, so it was retained descriptively but excluded from transferable broad-morphology modelling.

## Scientific conclusions

1. **Data curation is part of the modelling problem.** Bulk-state and morphology labels required source- and solvent-aware reconstruction before ML.
2. **Self-assembly is a molecule × environment problem.** Peptide chemistry and experimental conditions should be modelled together.
3. **Leakage-aware validation materially changes the meaning of performance.** Random row-wise splits are not suitable for claims about unseen peptide systems.
4. **Binary hydrogel prediction transfers strongly to unseen molecules**, although uncertainty must be interpreted at the molecular rather than row level.
5. **Three-class bulk-state prediction is substantially harder**, especially the distinction between organic non-gelling systems and organogels.
6. **Broad morphology is learnable, but independent class support is uneven.**
7. Current composition-based descriptors do not fully encode **residue order, three-dimensional packing or supramolecular interaction geometry**, which explains several analogue and composition-isomer errors.

## Fine-grained morphology: why modelling was stopped

A four-class fine-morphology dataset contained 257 condition rows from 57 molecular identities. A permanent unseen-molecule holdout was successfully reserved, but the remaining development data could not support stable three-fold molecularly independent cross-validation while maintaining minimum rare-class support.

Rather than weaken the leakage safeguards, predictive modelling was stopped. This is reported as an **independent-support limitation**, not as a failed classifier.

## Repository structure

```text
peptide-self-assembly-ml/
├── README.md
├── requirements.txt
├── notebooks/
│   └── Condition_Aware_Peptide_Self_Assembly_ML.ipynb
├── figures/
│   ├── figure_1_random_split_leakage.png
│   ├── figure_2_binary_holdout_roc.png
│   ├── figure_3_feature_block_importance.png
│   ├── figure_4_fully_aqueous_concentration_response.png
│   ├── figure_5_bulk3_confusion_matrix.png
│   ├── figure_6_broad_morphology_support.png
│   ├── figure_7_morphology_confusion_matrix.png
│   └── figure_S1_fine_morphology_support.png
└── data/
    └── README.md
```

## Reproducibility

The complete analysis is intentionally retained in **one master notebook**, divided into scientific sections covering data audit, curation, feature engineering, leakage analysis, binary modelling, three-class bulk-state modelling, morphology modelling, feasibility checks, artifact export and final conclusions.

To run locally:

```bash
pip install -r requirements.txt
jupyter notebook
```

Open `notebooks/Condition_Aware_Peptide_Self_Assembly_ML.ipynb`, restart the kernel and run all cells from top to bottom.

The notebook expects the source CSV files under `data/raw/`; see `data/README.md` for the expected filenames.

## Project status

**Analysis complete; manuscript/preprint preparation in progress.**

The repository will be updated with the final manuscript citation and archival DOI after preprint release.
