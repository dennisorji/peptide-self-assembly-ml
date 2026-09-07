# Data

The analysis combines condition-level peptide self-assembly records from **PeptideMiner** and **SAPdb**.

The master notebook expects the two source files at:

```text
data/raw/peptideminer_phase_data_clean.csv
data/raw/sapdb_v1.csv
```

These raw source files are not duplicated here until redistribution permissions/licensing are confirmed. Place your local copies in `data/raw/` before running the notebook from top to bottom.

The notebook reconstructs curated bulk-state and morphology targets, molecular identities, provenance fields and modelling tables directly from the source records. Generated analysis artifacts are written to `paper_outputs/` when the notebook is executed.
