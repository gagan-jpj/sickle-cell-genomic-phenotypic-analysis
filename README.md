
# Integrated Genomic–Phenotypic Analysis of Sickle Cell Disease

## Overview

This repository contains the computational workflows used to investigate the integration of genomic, phenotypic, demographic, complication, and laboratory information in a cohort of participants with sickle cell disease (SCD).

The project combines participant-level phenotype and laboratory information with phased genomic genotype data to investigate relationships between genetic variation and clinical characteristics of SCD.

The analysis is organised into four major stages:

1. Phenotypic, complication, and laboratory data processing
2. Phased genomic variant and genotype processing
3. Integrated genotype–phenotype association analysis
4. Unsupervised clustering and UMAP-based patient stratification

The notebooks are numbered according to the recommended analysis workflow.

---

## Research Objective

The primary objective of this computational workflow is to investigate whether integrating genomic information with phenotypic and clinical information can provide additional characterisation and stratification of disease-related clinical features compared with phenotype-based analysis alone.

The workflow evaluates:

* SCD complication profiles
* complication severity
* laboratory measurements
* genetic variation and carrier status
* genotype–phenotype associations
* genotype–laboratory associations
* multidimensional patient-level patterns
* unsupervised patient clustering

---

## Study Data

The analysis integrates several data modalities:

* demographic information
* SCD complication and phenotype information
* laboratory measurements
* phased genomic variant/genotype data
* derived genotype–phenotype datasets

The phenotype and laboratory workflow contains analyses based on the SCD cohort and generates participant-level intermediate datasets used in downstream analyses.

The genomic workflow processes phased whole-genome sequencing data at selected genomic loci and generates genotype, haplotype, carrier-frequency, and gene-level summaries.

### Cohort size

Different stages of the computational workflow contain cohort-specific participant counts. In particular, the genomic workflow contains analyses using a 481-participant genotype dataset, while earlier phenotype-processing steps include files and analyses based on a 476-participant cohort.

These cohort differences should be retained and explicitly documented rather than assuming that all analyses use an identical sample size.

---

# Analysis Workflow

```text
                    SCD STUDY COHORT
                           │
             ┌─────────────┴─────────────┐
             │                           │
             ▼                           ▼
      PHENOTYPE / LABS              GENOMIC DATA
             │                           │
             ▼                           ▼
    Complication processing       Phased VCF processing
    Severity assessment           Variant filtering
    Laboratory extraction         Genotype extraction
    Laboratory analysis           Haplotype summaries
             │                    Gene-level summaries
             │                           │
             └─────────────┬─────────────┘
                           │
                           ▼
                INTEGRATED DATASET
                           │
                           ▼
           GENOTYPE–PHENOTYPE ANALYSIS
                           │
              ┌────────────┼────────────┐
              │            │            │
              ▼            ▼            ▼
           Fisher       Logistic      Linear
          exact tests   regression   regression
              │            │            │
              └────────────┼────────────┘
                           ▼
                     FDR correction
                           │
                           ▼
                 UMAP / CLUSTERING
                           │
                           ▼
                Patient stratification
```

---

# Repository Structure

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── workflow_overview.md
│
├── notebooks/
│   ├── 01_phenotype_and_lab_processing.ipynb
│   ├── 02_phased_genomic_processing.ipynb
│   ├── 03_integrated_genotype_phenotype_analysis.ipynb
│   └── 04_umap_machine_learning.ipynb
│
└── data/
    └── README.md
```

---

# Notebook 01 — Phenotype and Laboratory Processing

**File:** `notebooks/01_phenotype_and_lab_processing.ipynb`

This notebook contains the processing and analysis of demographic, phenotypic, complication, and laboratory information.

The workflow includes:

* participant demographic processing
* SCD complication identification
* complication frequency analysis
* complication severity categorisation
* top-complication identification
* participant-level complication summaries
* laboratory data extraction
* laboratory measurements in long and wide formats
* laboratory data cleaning
* laboratory severity categorisation
* laboratory distributions and summaries
* complication–laboratory comparisons
* Mann–Whitney U testing
* generation of intermediate phenotype and laboratory datasets

Examples of generated intermediate datasets include:

* `SCD_Demographics.csv`
* `SCD_Complication_Severity_Categorised.csv`
* `SCD_Complication_Severity_Assessed.csv`
* `SCD_Top10_Complication_Details.csv`
* `SCD_Lab_Measurements_Long.csv`
* `SCD_Lab_Measurements_Wide.csv`
* `SCD_Complication_Lab_Severity_Stats.csv`
* `Median_Complication_Lab_Profiles.csv`

---

# Notebook 02 — Phased Genomic Processing

**File:** `notebooks/02_phased_genomic_processing.ipynb`

This notebook processes phased genomic data and generates participant-level genotype and gene-level summaries.

The workflow uses Hail and related genomic-processing tools to work with phased VCF data.

The analysis includes:

* initialisation of Hail
* access to phased genomic data
* selection of study participants
* selection of target genomic positions
* chromosome-specific processing
* filtering to selected loci and participants
* genotype extraction
* biallelic variant processing
* genotype matrix construction
* participant-level genotype tables
* variant summaries
* haplotype counting
* allele/carrier-frequency summaries
* gene-level dosage summaries

The notebook generates outputs including genotype-long and genotype-wide tables, variant summaries, and gene-level summary tables.

Examples include:

* `ALL_481_genotypes_long.csv`
* `ALL_481_genotypes_wide.csv`
* `ALL_481_variants_summary.csv`
* `ALL_481_variants_summary_with_haplotypes_and_genes.csv`
* `FINAL_SCD_481_21variant_table.csv`
* `SCD481_gene_dosage_matrix.csv`
* `SCD481_gene_summary_with_freqs.csv`

---

# Notebook 03 — Integrated Genotype–Phenotype Analysis

**File:** `notebooks/03_integrated_genotype_phenotype_analysis.ipynb`

This notebook integrates participant-level genomic genotype information with phenotype, complication, demographic, and laboratory datasets.

The workflow includes:

* loading phenotype datasets
* loading genotype data
* constructing unique variant identifiers
* transforming genotype data to participant-level format
* matching participant identifiers
* merging genotype and phenotype information
* quality-control checks
* carrier/non-carrier comparisons
* complication association analyses
* laboratory association analyses
* Fisher's exact tests
* logistic regression
* linear regression
* multiple-testing correction
* FDR-adjusted results
* ranking of statistically relevant findings

Important generated outputs include:

* `SCD_Genotype_Phenotype_Merged.csv`
* `SCD_Master_Analysis_Dataset.csv`
* `All_Complication_Fisher_Results.csv`
* `All_Complication_Fisher_Results_FDR.csv`
* `Pulmonary_Hypertension_Fisher_Results.csv`
* `Pulmonary_Hypertension_Logistic_Results.csv`
* `Lab_Complication_Results.csv`
* `Lab_Complication_Associations.csv`
* `Lab_Complication_Associations_FDR.csv`
* `Top20_Ranked_Findings.csv`
* `Publication_Top_Findings_Table.csv`

These files should **not automatically be uploaded to the public repository**, because they may contain participant-level or controlled-access information.

---

# Notebook 04 — UMAP and Machine Learning

**File:** `notebooks/04_umap_machine_learning.ipynb`

This notebook investigates patient-level structure using dimensionality reduction and unsupervised clustering.

The workflow includes:

* preparation of integrated genotype and phenotype features
* handling of missing values
* Gower-based feature processing
* clustering
* K-means clustering
* K-medoids analysis
* DBSCAN clustering
* silhouette-score assessment
* UMAP dimensionality reduction
* clinical cluster summaries
* genetic cluster summaries
* phenotype distributions
* UMAP visualisation
* cluster-level interpretation

Generated outputs include:

* `SCD_clustering_results_genetic.csv`
* `SCD_clustering_results_with_umap_clusters.csv`
* `cluster_genetic_frequency_summary.csv`
* `cluster_numeric_summary.csv`
* `umap_cluster_clinical_summary.csv`
* `umap_cluster_genetic_summary.csv`
* `umap_cluster_phenotype_counts.csv`

---

# Statistical Methods

The notebooks use several statistical and machine-learning approaches.

| Analysis                                    | Method                                |
| ------------------------------------------- | ------------------------------------- |
| Categorical genotype/phenotype associations | Fisher's exact test                   |
| Binary outcome modelling                    | Logistic regression                   |
| Continuous laboratory associations          | Linear regression                     |
| Laboratory comparisons between groups       | Mann–Whitney U test                   |
| Multiple testing                            | False Discovery Rate (FDR) correction |
| Patient clustering                          | K-means                               |
| Alternative clustering                      | K-medoids                             |
| Density-based clustering                    | DBSCAN                                |
| Dimensionality reduction                    | UMAP                                  |
| Feature-distance analysis                   | Gower distance                        |
| Cluster evaluation                          | Silhouette score                      |

The exact statistical implementation and variables are documented in the corresponding notebooks.

---

# Genomic Analysis

The phased genomic workflow analyses selected variants across SCD-relevant genomic regions and genes.

The current notebook includes variant and gene-level analysis involving targets including:

* HBB / HBB cluster
* HBG2
* BCL11A
* HBS1L-MYB
* TNF
* APOE
* APOL1
* VCAM1

The genomic notebook contains the definitive list of analysed positions and should be treated as the primary source for the exact variant definitions used in the analysis.

---

# Data Availability

Participant-level genomic, demographic, clinical, phenotypic, and laboratory data are not included in this public repository.

The repository is intended to contain computational code, documentation, and other outputs that are appropriate for public release.

Researchers attempting to reproduce the analyses must have appropriate authorised access to the underlying datasets and must configure the required input files within their authorised computational environment.

See `data/README.md` for further information.

---

# How to Run

The notebooks are intended to be executed in the order:

```text
01 → 02 → 03 → 04
```

However, individual notebooks may require specific input datasets generated by earlier analyses or available within the authorised research environment.

Before execution:

1. Obtain appropriate authorised access to the required study datasets.
2. Place or mount the required input data in the expected computational environment.
3. Review the file paths and environment variables used in the notebooks.
4. Install the required Python packages.
5. Execute the notebooks in the documented workflow order.

The genomic-processing notebook additionally requires the appropriate environment for Hail and access to the phased genomic data.

---

# Software Requirements

The computational workflow uses Python and packages including:

* pandas
* NumPy
* SciPy
* statsmodels
* scikit-learn
* matplotlib
* seaborn
* UMAP
* Gower
* pyclustering
* Hail
* Google Cloud BigQuery libraries

The versions used for the final analysis should be documented in `requirements.txt`.

---

# Reproducibility

The repository provides the computational workflows used for the reported analyses.

Complete reproduction of the analysis requires access to the underlying study data and the computational environment in which the genomic and clinical data can be accessed.

Notebook outputs and participant-level datasets should only be published when they have been confirmed to be suitable for public release.

For reproducibility, the repository documents:

* analysis order
* input data requirements
* computational methods
* statistical methods
* software dependencies
* generated outputs

---

# Compliance and Data Protection

This repository should not contain:

* participant identifiers
* identifiable clinical information
* controlled-access genomic data
* raw VCF files containing participant-level genotypes
* confidential research data
* credentials or authentication tokens
* private cloud-storage paths or credentials

Only code and data products that are permitted for public release should be committed to the repository.

---

# Research Paper

This repository supports the computational analyses associated with:

**[Insert final manuscript title]**

**Authors:**
[Insert authors]

**Journal:**
[Insert journal]

**DOI:**
[Insert DOI after publication]

---

# Citation

If you use the computational workflow or code in this repository, please cite the associated publication:

> [Insert final publication citation]

A `CITATION.cff` file may be added once the final authorship, title, and publication information have been confirmed.

---

# Author

**Gagandeep Kaur**

King's College London

2026


