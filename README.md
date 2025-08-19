# Yandex-Practicum: Hands-On Python, SQL, and Data Viz Projects 🚀

[![Releases - download](https://img.shields.io/badge/Releases-download-blue?logo=github)](https://github.com/Idrissa08/Yandex-Practicum/releases)

![Matplotlib](https://matplotlib.org/stable/_static/logo2_compressed.svg) ![Pandas](https://pandas.pydata.org/static/img/pandas.svg) ![Seaborn](https://seaborn.pydata.org/_static/logo-wide-lightbg.svg) ![Postgres](https://www.postgresql.org/media/img/about/press/elephant.png)

About
- Repository: Yandex-Practicum learning projects.
- Focus: practical, hands-on tasks that cover data cleaning, analysis, visualization, and SQL-backed workflows.
- Main tools: Python, pandas, NumPy, matplotlib, seaborn, scipy, statsmodels, SQL, PostgreSQL, SQLAlchemy, requests, Tableau.
- Goal: build repeatable project templates and worked examples you can adapt to your own data.

Quick link
- Download required release assets and execute the included script from the Releases page:
  https://github.com/Idrissa08/Yandex-Practicum/releases

Why this repo
- It groups short projects and exercises that mirror real-world tasks.
- Each project demonstrates a clear pipeline: ingest → clean → analyze → visualize → persist.
- You get code, sample data, and a runnable export for each exercise.

Contents (high level)
- projects/
  - 01-data-cleaning/          — ETL patterns in pandas, cleaning recipes
  - 02-exploratory-analysis/   — EDA notebooks, distribution checks, pivot tables
  - 03-visualization/          — matplotlib + seaborn examples, dashboard sketches
  - 04-time-series/            — decomposition, forecasting baselines
  - 05-statistics/             — hypothesis tests, regression with statsmodels
  - 06-sql-workshop/           — SQL schema, seeds, queries, SQLAlchemy integration
  - 07-api-scripts/            — requests examples and API ETL
  - notebooks/                 — polished Jupyter notebooks for each project
  - data/                      — small sample datasets (CSV, parquet)
  - sql/                       — schema, seed data, stored queries
  - docker/                    — Dockerfile and docker-compose for local dev
  - requirements.txt           — pip install list
  - environment.yml            — conda environment spec
  - README.md                  — this file

Badges and topics
- Topics applied: matplotlib, numpy, pandas, postgresql, python, requests, scipy, seaborn, sql, sqlalchemy, statsmodels, tableau
- Use badges to find examples and releases quickly.

Set up your environment

System requirements
- Python 3.9+ recommended.
- PostgreSQL 12+ for database-backed exercises.
- Docker if you want to run a containerized database or run notebooks in a container.

Python (pip)
- Create a venv and install dependencies:
```bash
python -m venv .venv
source .venv/bin/activate        # macOS / Linux
.venv\Scripts\activate           # Windows
pip install -r requirements.txt
```

Conda
```bash
conda env create -f environment.yml
conda activate yandex-practicum
```

Docker (optional)
- Launch a local Postgres instance:
```bash
docker-compose up -d
# then connect with psql or SQLAlchemy
```

Run the release artifact
- Visit the Releases page and download the asset listed for the version you want.
- The release includes a runnable script or archive with setup instructions.
- After download, extract the archive and execute the included script. Example:
```bash
# Linux / macOS
tar xf yandex-practicum-v1.0.tar.gz
cd yandex-practicum-v1.0
./run.sh

# Windows (PowerShell)
Expand-Archive .\yandex-practicum-v1.0.zip
cd yandex-practicum-v1.0
.\run.bat
```
- The release page: https://github.com/Idrissa08/Yandex-Practicum/releases

Data workflow patterns
- Ingest: read CSV, JSON, SQL, or API responses with pandas.read_* and requests.
- Clean: use vectorized operations, .astype, .str methods, and date parsing with to_datetime.
- Transform: use groupby, pivot_table, merge, and concat to build analysis tables.
- Persist: export cleaned tables to parquet or write to Postgres with SQLAlchemy.

Example: simple ETL snippet
```python
import pandas as pd
from sqlalchemy import create_engine

df = pd.read_csv("data/sales_sample.csv", parse_dates=["date"])
df["revenue"] = df["price"] * df["quantity"]
df = df.dropna(subset=["customer_id"])

engine = create_engine("postgresql://user:pass@localhost:5432/yandex")
df.to_sql("sales_clean", engine, if_exists="replace", index=False)
```

SQL & PostgreSQL
- Schema files live in sql/schema.sql.
- Seed data and example queries live in sql/seeds/ and sql/queries/.
- Use SQLAlchemy for programmatic access:
```python
from sqlalchemy import create_engine, text

engine = create_engine("postgresql://user:password@localhost:5432/yandex")
with engine.connect() as conn:
    result = conn.execute(text("SELECT COUNT(*) FROM sales_clean"))
    print(result.scalar())
```

Notebooks and reproducibility
- Notebooks use clear kernels and environment.yml to lock package versions.
- Each notebook includes a small README block and a data manifest.
- Use JupyterLab or nbviewer to open notebooks:
```bash
jupyter lab notebooks/
```

Visualization and dashboards
- Use matplotlib for fine-grained control and seaborn for statistics plots.
- Export figures to PNG or SVG for embedding.
- Example plot:
```python
import seaborn as sns
sns.histplot(df["revenue"], kde=True)
```
- For interactive dashboards, export cleaned data to CSV or a database and connect via Tableau. Templates and .hyper export examples live under projects/03-visualization/export/.

Statistical tests and modeling
- Use scipy.stats for tests and statsmodels for regression and inference.
- Example: linear regression with statsmodels:
```python
import statsmodels.formula.api as smf

model = smf.ols("revenue ~ price + quantity", data=df).fit()
print(model.summary())
```
- The repo contains worked examples for A/B testing, time series decomposition, and basic forecasting baselines.

APIs and automation
- Requests-based examples show pagination, rate-limit handling, and simple retry logic.
- Use structured logging and error handling for production scripts.

Testing and CI
- Unit tests for key functions live under tests/.
- Run tests with pytest:
```bash
pytest -q
```
- Sample GitHub Actions workflow shows how to run tests, build artifacts, and publish a release.

Code style and linting
- Follow PEP 8 for Python code.
- The repository includes a pre-configured .flake8 and isort config.

How to contribute
- Fork the repo.
- Create a topic branch for your change.
- Add a clear commit message.
- Open a pull request against main with a short description and any data notes.
- Provide tests for new utilities or core behaviors.

Releases and artifacts
- The Releases page hosts packaged versions and runnable artifacts.
- For a packaged release, download the asset and run the included script to reproduce the environment and demo runs.
- If a release link is not available or does not work, check the Releases section on GitHub for the latest assets and instructions:
  https://github.com/Idrissa08/Yandex-Practicum/releases

Images and figures
- Plots and charts used in notebooks come from the visualization folder.
- You can preview sample output images in projects/03-visualization/figures/.
- The repo uses open logos from upstream projects for visual context.

Security and credentials
- Do not commit secrets. Use environment variables or secrets managers for DB credentials.
- Example connection pattern with env var:
```python
import os
from sqlalchemy import create_engine

url = os.getenv("DATABASE_URL")
engine = create_engine(url)
```

Licensing
- The repository includes a LICENSE file. Check it before reuse.

Resources and learning links
- Matplotlib docs: https://matplotlib.org
- Pandas docs: https://pandas.pydata.org
- Seaborn docs: https://seaborn.pydata.org
- PostgreSQL: https://www.postgresql.org
- Statsmodels: https://www.statsmodels.org

Acknowledgments
- The structure follows common industry workflows used in data science bootcamps and practical courses.
- External libraries and logos belong to their respective projects.

Contact and maintainers
- Maintainer: repository owner (see GitHub profile).
- Use issues to report bugs or request features.

Deploy and run examples
- Many examples run locally with the provided requirements file.
- For DB-backed examples, launch Postgres and run sql/schema.sql to create tables, then run seed scripts.

Troubleshooting
- If a package fails to install, try a matching Python minor version from environment.yml.
- For database connection errors, confirm Docker or local Postgres runs and the credentials match.

Appendix: common commands
- Install deps: pip install -r requirements.txt
- Run notebooks: jupyter lab notebooks/
- Run tests: pytest
- Run release script (after download): ./run.sh or .\run.bat

Credits
- Project templates and examples draw on open-source libraries and community guides for data workflows.