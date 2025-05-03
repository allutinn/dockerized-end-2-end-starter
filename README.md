# 🧱 Barebones Analytics Stack

(AI generated)

A minimal but production-ready local analytics pipeline that includes:

- **Python** for custom data extraction  
- **dbt** for SQL-based data transformations  
- **DuckDB** as a fast, file-based analytical database  
- **Apache Airflow** for orchestrating ETL workflows  
- **Apache Superset** for interactive dashboards and exploration  
- **Docker Compose** for isolated, containerized development

---

## 📁 Project Structure

\`\`\`
.
├── airflow/              # Airflow setup and DAGs
│   ├── dags/
│   └── Dockerfile
├── data/                 # DuckDB database & raw data
│   ├── raw/
│   ├── landing/
│   └── db/
├── dbt_wh/               # dbt project (models, macros, seeds, snapshots)
│   ├── models/
│   ├── macros/
│   ├── snapshots/
│   ├── profiles.yml
│   ├── dbt_project.yml
│   └── Dockerfile
├── extract/              # Python scripts for data extraction
│   ├── test_extract.py
│   ├── requirements.txt
│   └── Dockerfile
├── superset/             # Superset Dockerfile (with DuckDB support)
│   └── Dockerfile
├── util/                 # Optional scripts/utilities
├── docker-compose.yml    # Main Docker Compose orchestrator
└── .gitignore
\`\`\`

---

## 🚀 Quick Start

Clone and launch the stack:

\`\`\`bash
git clone <this_repo>
cd <this_repo>
docker-compose up --build
\`\`\`

### Interfaces:

- Superset: [http://localhost:8088](http://localhost:8088)  
- Airflow: [http://localhost:8080](http://localhost:8080)

---

## ⚙️ Run the ETL Process

### Option A: From Airflow UI

1. Open http://localhost:8080  
2. Trigger the DAG: \`extract_then_dbt\`

### Option B: Manually from Docker

\`\`\`bash
# Enter the extract container
docker-compose exec extractor bash
python extract/test_extract.py

# Enter the dbt container
docker-compose exec dbt_wh bash
dbt run --project-dir /app/dbt_wh
\`\`\`

---

## 📊 Visualize in Superset

1. Visit http://localhost:8088  
2. Log in (admin/admin)  
3. Connect a database: \`duckdb:///app/data/db/warehouse.duckdb\`  
4. Explore and visualize your models!
