# Data Availability

The genotype, phenotype, and clinical data used in this project were accessed
through the **All of Us Research Program Researcher Workbench**, under the
**Controlled Tier** data use policy.

## Why the data isn't in this repository

Per the [All of Us Data and Statistics Dissemination Policy](https://www.researchallofus.org/policy/data-and-statistics-dissemination-policy/),
participant-level data — including genotypes, phenotypes, demographics, and
any derived tables with small cell counts — **cannot be exported or shared
outside the Researcher Workbench**, including on public code repositories.
Only code, methods, and aggregate results that meet the program's dissemination
rules (e.g. minimum cell-size thresholds) may be shared publicly.

This repository therefore contains **analysis code only**. No participant-level
data, workspace bucket paths, project IDs, or credentials are included.

## How to reproduce this analysis

1. Apply for access to the All of Us Research Program at
   [researchallofus.org](https://www.researchallofus.org/) and request
   Controlled Tier access.
2. Recreate the cohort using the concept IDs and query logic documented in
   `notebooks/pheno.ipynb` (sickle cell disease cohort definition,
   complication concept IDs, and lab measurement concept IDs are all listed
   in-code).
3. Set your own `GOOGLE_PROJECT`, `WORKSPACE_BUCKET`, and `WORKSPACE_CDR`
   environment variables inside your own Researcher Workbench environment
   (placeholders are used throughout this repo's notebooks).
4. Run the notebooks in this order:
   - `phased.ipynb` — extracts phased short-read WGS genotype calls at target
     positions from the AoU controlled-tier VCFs.
   - `pheno.ipynb` — defines the sickle cell disease (SCD) cohort, pulls
     demographics, and derives complication/severity phenotypes.
   - `pheno_geno.ipynb` — merges the phased genotype calls with the phenotype
     and complication data into a single analysis dataset.
   - `UMAP_machine_learning.ipynb` — runs UMAP dimensionality reduction and
     k-medoids/k-means clustering on the merged dataset, and summarizes
     cluster-level clinical characteristics.

## Concept IDs

All OMOP concept IDs used to define the cohort, complications, and lab tests
are public vocabulary identifiers (not participant data) and are documented
directly in the notebook code for full reproducibility.
