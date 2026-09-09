# sickle-cell-genomic-phenotypic-analysis
Code and computational workflows for integrated genomic and phenotypic analysis.
# Integrated Genomic–Phenotypic Analysis of Sickle Cell Disease

This repository contains the computational workflows used to analyse genomic, phenotypic, demographic, laboratory, and complication data from a cohort of participants with sickle cell disease (SCD).

The project investigates whether integrating genomic information with phenotypic and clinical information can further stratify disease complications and related clinical characteristics compared with phenotype-based analysis alone.

## Overview

The analysis workflow consists of four principal stages:

1. **Phenotypic and clinical data processing**
2. **Genomic variant and genotype processing**
3. **Integrated genotype–phenotype analysis**
4. **Unsupervised clustering and UMAP-based analysis**

The notebooks are numbered according to the recommended analysis order.

---

## Repository structure

```text
.
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── .gitignore
│
├── notebooks/
│   ├── 01_phenotype_processing.ipynb
│   ├── 02_genomic_processing.ipynb
│   ├── 03_integrated_genotype_phenotype_analysis.ipynb
│   └── 04_umap_machine_learning.ipynb
│
├── data/
│   └── README.md
│
├── src/
│   └── README.md
│
├── results/
│   ├── figures/
│   └── tables/
│
└── docs/
    └── workflow.md
```

---

## Analysis workflow

### 1. Phenotype processing

`notebooks/01_phenotype_processing.ipynb`

This notebook processes the phenotypic and clinical information used in the study.

The workflow includes processing of:

* SCD complications
* complication severity
* complication counts
* demographic information
* laboratory measurements
* complication categories
* laboratory profiles across clinical severity groups

The outputs from this stage are used as inputs to subsequent integrated analyses.

---

### 2. Genomic processing

`notebooks/02_genomic_processing.ipynb`

This notebook processes phased genomic variant data and generates genotype-level and gene-level summaries.

The workflow includes:

* extraction of phased variant data
* processing of VCF files
* variant inspection
* conversion of multiallelic variants to biallelic representations
* removal of duplicate variants where appropriate
* genotype extraction
* genotype frequency summaries
* haplotype counts
* carrier-frequency calculations
* gene-level summaries

The genomic workflow uses tools including Hail, bcftools, pandas, NumPy, and related computational tools.

---

### 3. Integrated genotype–phenotype analysis

`notebooks/03_integrated_genotype_phenotype_analysis.ipynb`

This notebook combines genomic information with phenotypic, complication, demographic, and laboratory data.

The analysis includes:

* construction of integrated genotype–phenotype datasets
* carrier/non-carrier comparisons
* complication associations
* laboratory associations
* Fisher's exact tests
* logistic regression analyses
* multiple-testing correction
* FDR-adjusted results
* ranking and summarisation of principal findings

The resulting tables provide the statistical results used for interpretation and reporting.

---

### 4. UMAP and machine-learning analysis

`notebooks/04_umap_machine_learning.ipynb`

This notebook investigates clustering and dimensionality-reduction approaches using the available genomic and phenotypic information.

The workflow includes:

* genetic clustering
* UMAP dimensionality reduction
* cluster-level clinical summaries
* phenotype distributions
* genetic summaries
* comparison of clustering patterns

The purpose of this analysis is to investigate whether integrated information provides meaningful patient stratification beyond phenotype-only approaches.

---

## Data availability

The underlying participant-level genomic and clinical/phenotypic datasets are not included in this public repository because they may contain controlled-access human genomic or clinical information.

See [`data/README.md`](data/README.md) for information about the data sources and access requirements.

---

## Software and dependencies

The analyses were performed using Python-based computational workflows together with specialised genomic-analysis tools.

Major packages/tools used across the notebooks include:

* Python
* pandas
* NumPy
* SciPy
* scikit-learn
* UMAP
* Matplotlib
* Seaborn
* Hail
* bcftools
* PLINK

The specific software requirements are documented in `requirements.txt` and the relevant notebook.

---

## Reproducibility

The notebooks are provided in analysis order and contain the computational steps used to generate the reported analyses.

Because the underlying study data are controlled-access, complete reproduction requires authorised access to the original input datasets.

Before running the notebooks, ensure that the required input files are available and that the file paths in the notebooks have been configured for the local computational environment.

---

## Results

Derived figures and tables that are appropriate for public release are provided in:

```text
results/figures/
results/tables/
```

Participant-level or otherwise restricted data are not included.

---

## Research paper

This repository supports the analyses reported in:

Genomic Information Alters Phenotypic Stratification of Sickle Cell Disease Severity: An Exploratory Genomic-Phenotypic Analysis Using the All of Us Research Program

Authors:

Gagandeep Kaur 



---

## Citation

If you use this repository or the associated computational workflow, please cite the accompanying publication:

**[Insert citation after publication]**

A machine-readable citation file is provided in `CITATION.cff`.

---

## Contact

For questions regarding the computational workflow, please contact:

**[Insert appropriate research contact]**
