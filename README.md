# Robust Normality Modeling for Unsupervised Industrial Visual Anomaly Detection

### Under Training-Set Contamination and Intra-Class Variation

An empirical investigation of how controlled training-set contamination affects PatchCore's learned normality representation, memory-bank composition, nearest-neighbour retrieval behaviour, and anomaly scores.

## 1. Research Overview

Industrial visual anomaly detection commonly relies on learning representations of defect-free samples and identifying deviations during inference.

This study investigates whether training-set contamination changes the internal normality representation learned by PatchCore, even when aggregate detection performance remains stable.

The research focuses on the distinction between aggregate detection metrics and sample-level or memory-level behavioural changes.

## 2. Experimental Setup

| Component | Configuration |
|---|---|
| Dataset | MVTec AD |
| Category | Bottle |
| Detection framework | Unsupervised anomaly detection |
| Model | PatchCore |
| Backbone | ImageNet-pretrained WideResNet50 |
| Feature layers | Layer 2 and Layer 3 |
| Clean training images | 209 |
| Test images | 83 |
| Contamination levels | 0%, 5%, 10%, 20% |
| Actual contaminated images | 0, 10, 21, 41 |
| Test set | Fixed across experiments |

The contaminated training conditions were generated synthetically. The test set remained unchanged.

## 3. Repository Structure

```text
patchcore-robustness-under-training-contamination/
│
├── notebooks/
│   ├── 01_clean_baseline.ipynb
│   ├── 02_contamination_experiments.ipynb
│   └── 03_mechanism_analysis.ipynb
│
├── results/
├── manuscript/
├── README.md
└── .gitignore
```

## 4. Experimental Workflow

The experiments are organized into three stages:

**Notebook 01 — Clean PatchCore Baseline**

Establishes the reference model using defect-free Bottle training images and evaluates its performance on the fixed test set.

**Notebook 02 — Controlled Training-Set Contamination**

Investigates PatchCore under increasing contamination levels of 5%, 10%, and 20%, while maintaining the same test set and primary model configuration.

**Notebook 03 — Mechanism Analysis**

Investigates:
- Memory-bank composition and provenance.
- Nearest-neighbour retrieval changes.
- Retrieval of contaminated-source features.
- Individual anomaly-score variations.
- Image-ranking stability.
- Retrieval change versus score change.
- Representative anomaly-map comparisons.

Execute the notebooks in the order listed above.

## 5. Key Experimental Findings

| Contamination | Instance AUROC | Full Pixel AUROC | Anomaly Pixel AUROC |
|---|---:|---:|---:|
| 0% | 1.000000 | 0.984839 | 0.979561 |
| 5% | 1.000000 | 0.984991 | 0.979764 |
| 10% | 1.000000 | 0.985076 | 0.979881 |
| 20% | 1.000000 | 0.985292 | 0.980171 |

Additional observations:

- The retained memory bank increased from 16,385 vectors in the clean condition to 19,600 vectors at 20% contamination.
- Nearest-neighbour retrieval identities changed substantially relative to the clean model.
- Contaminated-source feature vectors were retained and retrieved during inference.
- Individual anomaly scores and image rankings changed despite stable aggregate AUROC.
- Retrieval change and anomaly-score change did not show a statistically significant association in the reported correlation analysis.

These findings indicate that aggregate performance metrics alone do not fully describe changes in PatchCore's internal reference representation and sample-level responses.

## 6. Dataset

This project uses the Bottle category of the MVTec Anomaly Detection (MVTec AD) dataset.

The dataset is not redistributed in this repository.

Obtain the dataset through the official source:

https://www.mvtec.com/company/research/datasets/mvtec-ad

Expected directory structure:

```text
bottle/
├── ground_truth/
├── train/
│   └── good/
├── test/
│   ├── good/
│   ├── broken_large/
│   ├── broken_small/
│   └── contamination/
├── license.txt
└── readme.txt
```

Please consult the official dataset licensing terms before downloading or using the data.

## 7. Limitations

This study has the following limitations:

- Evaluation is restricted to one MVTec AD category: Bottle.
- Only one primary PatchCore configuration is investigated.
- Training contamination is synthetically generated.
- Intra-class variation is analysed descriptively rather than independently manipulated.
- The findings do not establish general robustness across datasets, categories, or industrial environments.

## 8. Research Manuscript

The accompanying research manuscript will be provided in the `manuscript/` directory following its final publication-readiness checks.

## 9. Acknowledgements

This work builds upon the PatchCore approach and the MVTec AD benchmark.

Original PatchCore implementation:

https://github.com/amazon-science/patchcore-inspection

Dataset reference:

Bergmann et al., MVTec AD: A Comprehensive Real-World Dataset for Unsupervised Anomaly Detection.

Please refer to the original publications and their licensing terms when using the method or dataset.

## 10. Research Scope

The objective is to study the behaviour of an unsupervised normality-modelling approach under controlled training-set contamination, with particular attention to memory representation, nearest-neighbour retrieval, and sample-level anomaly responses.
