# DataSentinel
### Intelligent Data Reliability & Trust Platform

**Detect unreliable data. Investigate failures. Recover safely. Verify the result.**

DataSentinel is a data engineering project designed to help teams identify data quality problems, understand pipeline failures, assess data trustworthiness, and recover from incidents with evidence-based verification.

The long-term goal is to connect data quality monitoring, dataset lineage, root-cause analysis, and safe pipeline recovery in one platform.

> **Project status:** Early development — the initial CLI-based data trust engine is being built.

## The Problem

Data pipelines can complete successfully while producing incomplete, duplicated, stale, or incorrect data. Traditional validation checks may identify a problem without explaining its downstream impact or helping engineers recover safely.

DataSentinel aims to address these challenges by providing:

- **Data quality monitoring:** Detect missing values, duplicate keys, invalid records, and schema violations.
- **Data trust assessment:** Calculate transparent quality metrics and explain why a dataset is trusted or degraded.
- **Data lineage:** Track upstream and downstream dataset dependencies.
- **Root-cause analysis:** Correlate quality failures and pipeline incidents with supporting evidence.
- **Safe recovery:** Plan, approve, and execute controlled recovery actions.
- **Post-recovery verification:** Recheck data quality and reconcile results before restoring trusted status.
- **GenAI-assisted investigation:** Explain incidents using recorded evidence and approved data definitions.

These capabilities will be implemented incrementally and tested against deliberately injected data failures.

## Core Architecture

```text
Data Sources
  MySQL | CSV | JSON
          |
          v
Python Ingestion & Pydantic Validation
          |
          v
DataSentinel Core Engine
  ├── Data Trust Engine
  ├── Data Quality Checks
  ├── Dataset Lineage
  ├── Incident Diagnosis
  ├── Recovery Planning
  └── Verification Engine
          |
          v
MySQL Metadata Store
  ├── Scan History
  ├── Quality Check Results
  ├── Record-Level Issues
  └── Incident & Recovery History
          |
          v
CLI → Future Dashboard → GenAI Assistant
```

### Planned Lakehouse and Cloud Integration

```text
MySQL / Files
      |
      v
Azure Data Lake Storage
      |
      v
Databricks + PySpark
  Bronze → Silver → Gold
      |
      v
Snowflake + Snowpark + dbt
      |
      v
Trusted Analytics & Business Applications
```

The lakehouse and cloud components are planned extensions, not prerequisites for the initial local MVP.

## Technology Stack

| Area | Technologies |
|---|---|
| Programming | Python |
| Data validation | Pydantic |
| Data manipulation and analysis | pandas |
| Visualization | Matplotlib, Seaborn |
| Metadata storage | MySQL |
| Distributed processing | Hadoop, PySpark |
| Lakehouse platform | Databricks, Delta Lake |
| Cloud platform | Microsoft Azure |
| Data warehouse | Snowflake |
| Warehouse-side Python | Snowpark |
| Transformation and testing | dbt |
| Version control | Git, GitHub |
| CI/CD | GitHub Actions |
| Containers | Docker |
| Orchestration and deployment | Kubernetes |
| Work and incident management | Jira, ServiceNow |
| AI-assisted investigation | GenAI |

Technologies will be introduced when they have a clear role in the architecture.

## Initial MVP

The first milestone is a lightweight CLI-based data trust engine running on Linux.

It will:

1. Read a retail sales CSV file.
2. Validate required fields and data types using Pydantic.
3. Detect duplicate transaction identifiers.
4. Identify invalid dates, missing identifiers, and non-positive transaction amounts.
5. Calculate completeness, validity, uniqueness, and an aggregate trust score.
6. Assign a trust status based on explicit rules.
7. Persist scan runs, quality checks, and record-level issues in MySQL.
8. Display reports through the command line.

### Example Dataset

The initial sample contains deliberately injected failures:

- Duplicate transaction IDs.
- Missing customer identifiers.
- Negative transaction amounts.
- Invalid transaction dates.

The purpose is to test whether the engine detects these conditions consistently.

## Development Roadmap

- [ ] **Phase 1 — Data Trust CLI:** CSV ingestion, validation, trust metrics, MySQL persistence, automated tests.
- [ ] **Phase 2 — Trust Policies:** Configurable thresholds, severity levels, and dataset-specific rules.
- [ ] **Phase 3 — Dataset Lineage:** Upstream/downstream dependency tracking and impact analysis.
- [ ] **Phase 4 — Incident Diagnosis:** Failure correlation, evidence collection, and root-cause recommendations.
- [ ] **Phase 5 — Safe Recovery:** Approval workflows, idempotent replay, and post-recovery verification.
- [ ] **Phase 6 — Data Platform Integration:** PySpark, Databricks, Azure, Snowflake, Snowpark, and dbt.
- [ ] **Phase 7 — DataOps:** Automated testing, Docker packaging, deployment, monitoring, and incident integrations.
- [ ] **Phase 8 — GenAI & UI:** A dashboard and evidence-grounded assistant for incident investigation.

## Getting Started

### Prerequisites

- Linux (CentOS or a compatible distribution)
- Python 3
- MySQL Server
- Git

### 1. Clone the repository

Replace `YOUR_GITHUB_USERNAME` with your GitHub username.

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/DataSentinel.git
cd DataSentinel
```

### 2. Create a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

Once the implementation and `requirements.txt` have been committed:

```bash
pip install -r requirements.txt
```

### 4. Configure MySQL

Create a database named `datasentinel` and configure a dedicated application user. Store credentials in a local `.env` file and never commit secrets.

### 5. Run the CLI

The following commands will be available once the corresponding CLI implementation is committed:

```bash
python datasentinel.py init-db
python datasentinel.py scan sample_data/sales.csv
python datasentinel.py report RUN_ID
```

Replace `RUN_ID` with the scan ID returned by the application.

## Engineering Principles

DataSentinel is being developed around these principles:

- **Correctness before automation:** Detect and understand failures before attempting recovery.
- **Idempotency:** Reprocessing the same batch must not silently double-count business events.
- **Explicit trust rules:** Scores must be explainable and must not hide critical failures.
- **Evidence-based diagnosis:** Recommendations should reference observable checks, logs, and lineage.
- **Controlled recovery:** Risky changes require approval and an audit trail.
- **Reproducible testing:** Failure scenarios should be repeatable and measurable.
- **Least privilege:** Credentials and data access should be restricted to what each component needs.

## Evaluation Metrics

The platform will be evaluated using measurable engineering criteria:

- Data validation precision and false-positive rate.
- Duplicate detection accuracy.
- Source-to-target reconciliation accuracy.
- Incident detection latency.
- Root-cause recommendation quality.
- Recovery success rate.
- Post-recovery correctness.
- Processing time and resource overhead.

Performance and reliability claims will be documented only after running reproducible experiments.

## Contributing

This is an evolving engineering project. Contributions, issue reports, design feedback, and reproducible bug reports are welcome.

## License

No open-source license has been selected yet. Until a license is added, reuse and redistribution are subject to applicable copyright law.

---

**DataSentinel — Making data pipelines more trustworthy, explainable, and recoverable.**
