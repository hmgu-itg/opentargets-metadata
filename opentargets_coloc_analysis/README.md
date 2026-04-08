# OpenTargets Coloc Analysis (Scaffold)

## Status

This directory contains an early-stage Python package scaffold for GWAS-QTL colocalization extraction and summary tooling.

It is not yet a fully aligned, production-ready CLI package. The top-level script `../coloc_extract.py` is currently the maintained runnable workflow.

## Current Contents

- `src/cli.py`: argument parsing entry point draft
- `src/main.py`: pipeline orchestration draft
- `src/coloc/extract.py`: query/extract helper functions
- `src/coloc/summary.py`: summary helper prototype
- `setup.py`: package metadata draft
- `requirements.txt`: local package dependencies

## Installation

From this directory:

```bash
pip install -r requirements.txt
```

## Usage Notes

- The module structure and imports are still being normalized.
- CLI examples previously documented here may not run without additional packaging/import fixes.
- For reproducible extraction runs, use the top-level script:

```bash
python ../coloc_extract.py --help
```

## Dependencies

Dependencies currently listed in `requirements.txt`:
- DuckDB
- pyarrow
- pandas
- numpy
- argparse
- scikit-learn
- matplotlib
- seaborn

## License

This subdirectory follows the repository-level MIT license. See `../LICENSE`.