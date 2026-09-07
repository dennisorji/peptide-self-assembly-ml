# Data

This analysis combines condition-level peptide self-assembly records from **PeptideMiner** and **SAPdb**.

## Expected local files

Place the source data under `data/raw/` with these filenames:

```text
data/raw/peptideminer_phase_data_clean.csv
data/raw/sapdb_v1.csv
```

The `data/raw/` directory is excluded from Git so that upstream datasets are not redistributed without preserving their original terms and provenance.

## PeptideMiner

Source repository: https://github.com/lamm-mit/PeptideMiner

PeptideMiner provides a cleaned self-assembly phase dataset under its `data/` directory. The analysis uses the condition-level phase data and expects the local copy to be named:

```text
peptideminer_phase_data_clean.csv
```

## SAPdb

Official database: https://webs.iiitd.edu.in/raghava/sapdb/

SAPdb v1 archive: https://doi.org/10.5281/zenodo.20078457

Reference:

> Mathur D, Kaur H, Dhall A, Sharma N, Raghava GPS. SAPdb: A database of short peptides and the corresponding nanostructures formed by self-assembly. *Computers in Biology and Medicine*. 2021;133:104391. https://doi.org/10.1016/j.compbiomed.2021.104391

Use the SAPdb v1 data corresponding to the 1,049-entry database and place the CSV used for the analysis at:

```text
sapdb_v1.csv
```

## Generated data

The notebook performs the curation and integration steps programmatically, including:

- bulk-state reconstruction;
- morphology reconciliation and confidence assignment;
- chemically meaningful molecular-identity construction;
- publication/provenance mapping;
- feature construction;
- modelling-table generation.

Generated datasets and result tables are written to `paper_outputs/` when the analysis is executed.
