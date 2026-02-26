Here’s a clean README.md you can paste in (fits your DVC + GitHub Actions exercise and your current repo structure):

# MLE: GitHub Actions + CI/CD (with DVC)

This repository is a small learning project to practice:

- **GitHub Actions** for CI (running tests on pull requests)
- **Branch protection + PR workflow**
- **DVC** (Data Version Control) to track large data files without committing them to Git
- Basic Python package structure (`src/` + `tests/`)

---

## Repository structure

- `.github/workflows/test.yml` — GitHub Actions workflow that runs `pytest`
- `src/` — source code (example: `src/calculator.py`)
- `tests/` — unit tests (example: `tests/test_calculator.py`)
- `data/` — local data folder (large files are tracked via DVC, not Git)
- `.dvc/` — DVC configuration and cache metadata

---

## Setup

Create and activate a virtual environment, then install dependencies:

```bash
python -m venv .venv
source .venv/bin/activate  # (mac/linux)
pip install -r requirements.txt
Run tests locally:

python -m pytest -q
Data versioning with DVC
This repo uses DVC to track the NYC TLC Green Taxi dataset (January 2025):

https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page

Download example:

wget -P ./data https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-01.parquet
Track with DVC:

dvc add data/green_tripdata_2025-01.parquet
git add data/green_tripdata_2025-01.parquet.dvc .gitignore
git commit -m "Track dataset with DVC"
DVC remote (Google Cloud Storage)
A GCS bucket is used as the DVC remote. Configure (example):

dvc remote add -d myremote gs://<your-bucket-name>/
git add .dvc/config
git commit -m "Configure DVC GCS remote"
Push/pull data:

dvc push
dvc pull
Note: Do not commit credentials. Use .dvc/config.local for local-only auth settings.

CI (GitHub Actions)
On every Pull Request to main, GitHub Actions runs:

dependency installation
pytest
You can view runs under the Actions tab of the repository.

