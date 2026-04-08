# OpenTargets Data Analysis

## Overview

This repository contains exploratory analysis code and generated metadata derived from OpenTargets data exports.

Current repository contents include:
- notebook-based analyses in `opentargets_coloc_analysis.ipynb`
- a script-based extraction workflow in `coloc_extract.py`
- metadata artifacts under `metadata/` (CSV, JSON, and manifest outputs)
- utility scripts under `utils/` for catalog conversion and validation

## Repository Structure

- `coloc_extract.py`: DuckDB-based extraction script for colocalization data with configurable thresholds and outputs
- `metadata/`: Generated outputs and dataset metadata snapshots
- `utils/`: Helper utilities (`convert_catalog.py`, `catalog_summary.py`, `verify_catalog.py`)
- `opentargets_coloc_analysis/`: Separate coloc-analysis package scaffold (work in progress)

## Environment

Top-level Python requirements are pinned in `requirements.txt`:
- duckdb==1.1.3
- pyarrow==17.0.0

Recommended Python version: 3.11.x

Install:

```bash
pip install -r requirements.txt
```

## Running The Script Workflow

The currently maintained script entry point is `coloc_extract.py`.

Example:

```bash
python coloc_extract.py \
  --data-root /path/to/parquet_root \
  --h4-threshold 0.8 \
  --out-dir /path/to/output_dir \
  --stats-out /path/to/output_dir/summary_stats.parquet
```

This script expects these parquet files under `--data-root`:
- `colocalisation_coloc.parquet`
- `credible_set.parquet`
- `study.parquet`

## Generated Outputs

The repository currently contains generated examples such as:
- `metadata/csv/colocalisation_available_columns_with_variants.csv`
- `metadata/csv/gene_drug_target_associations.csv`
- `metadata/csv/colocalisation_drug_association_snapshot.csv`

## Data Source

- [OpenTargets Platform](https://platform.opentargets.org/)

## Data Availability And Provenance

### Data Availability

- This repository contains derived metadata artifacts under `metadata/` (CSV/JSON/manifests), not the full raw OpenTargets parquet releases.
- Raw source data should be obtained from official OpenTargets releases (OpenTargets Platform and OpenTargets Genetics documentation/download channels).
- The analyses in this repository were developed against OpenTargets release path conventions consistent with `data_version_29_07` (29.07), and outputs may differ when regenerated from newer releases.

### Provenance

- `metadata/columns_manifest.json` documents selected columns for key datasets used in downstream extraction.
- `coloc_extract.py` writes both `query.sql` and `schema.json` into the run output directory, providing SQL/query and schema provenance for each extraction run.
- Derived snapshots currently tracked in this repo include:
  - `metadata/csv/colocalisation_available_columns_with_variants.csv`
  - `metadata/csv/gene_drug_target_associations.csv`
  - `metadata/csv/colocalisation_drug_association_snapshot.csv`

### Regeneration

1. Install pinned dependencies:

  ```bash
  pip install -r requirements.txt
  ```

2. Prepare a data root containing at minimum:
  - `colocalisation_coloc.parquet`
  - `credible_set.parquet`
  - `study.parquet`

3. Run extraction:

  ```bash
  python coloc_extract.py \
    --data-root /path/to/parquet_root \
    --h4-threshold 0.8 \
    --out-dir /path/to/output_dir \
    --stats-out /path/to/output_dir/summary_stats.parquet
  ```

4. Archive the generated `query.sql` and `schema.json` together with output tables for complete run-level provenance.

## License

This repository is licensed under the MIT License. See `LICENSE`.
