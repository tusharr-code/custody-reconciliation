# Custody Reconciliation Workbench

**Automating Transaction Reconciliation, Position Reconciliation and Break Management**

A full-stack financial operations application that streamlines reconciliation between custodian records and internal accounting books.

Built to demonstrate how financial domain knowledge and modern technology can improve reconciliation workflows, exception investigation and operational efficiency.

**Developed by:** Tushar Ramugade
**GitHub Repository:** https://github.com/tusharr-code/custody-reconciliation-workbench

---

## Project Overview

In investment operations, reconciliation teams regularly compare custodian statements against internal accounting records to identify discrepancies, investigate exceptions and resolve outstanding breaks.

Traditional reconciliation processes can involve significant manual effort, fragmented workflows and limited visibility into unresolved exceptions.

The Custody Reconciliation Workbench explores a technology-driven approach to these challenges through automated matching, break identification and centralised exception management.

---

## Key Features

### 1. Transaction Reconciliation
- Compare custodian and internal transaction records.
- Identify matched and unmatched transactions.
- Highlight records missing from either side.
- Identify quantity, price, amount, currency, trade date and settlement date discrepancies.
- Configurable matching keys and tolerances (quantity, price, amount, date).

### 2. Position Reconciliation
- Compare security-level holdings between custodian and internal books.
- Identify quantity differences and market value discrepancies.
- Identify securities missing from either source.
- Dated position snapshots stored for position history.

### 3. Break Management
- Centralised exception management with persistent break records.
- Track open, investigating, pending-custodian and resolved breaks.
- Record root causes, owners and investigation comments.
- Audit event trail for run creation and break updates.

### 4. Data Ingestion and Processing
- Upload reconciliation input files in CSV format.
- Flexible column aliases (for example `qty`, `ccy`, `trade_id`, `ticker`).
- Validate incoming records and report row-level errors.
- Combined files containing both `TRANSACTION` and `POSITION` rows are filtered automatically by the selected reconciliation type.
- Process data using Python, Pandas and Decimal-based matching logic.

### 5. Reporting and Export
- Review complete matched and break results for every run.
- Browse saved reconciliation runs and position history.
- Export break records as CSV for operational review.

---

## Application Screenshots

### Dashboard
<img width="1917" height="1022" alt="Position histody " src="https://github.com/user-attachments/assets/295c162c-0505-46d2-898f-781bec20c757" />


### Transaction Reconciliation
<img width="1916" height="1017" alt="Transactions" src="https://github.com/user-attachments/assets/7b1dd669-0094-433b-acde-86a33df45fae" />

### Position Reconciliation
<img width="1916" height="1010" alt="Position" src="https://github.com/user-attachments/assets/b2fc6023-2097-44d0-b220-2767416fd3b5" />


### Break Management

<img width="1862" height="1000" alt="open breaks" src="https://github.com/user-attachments/assets/3301154e-d3e3-44ef-b4a9-172e53d3730e" />

Video :

https://www.youtube.com/watch?v=UIKlOz5USo0
---

## Technology Stack

| Component | Technology |
|---|---|
| Frontend | React, Vite |
| Backend | Python, FastAPI |
| Database | PostgreSQL 16, SQLAlchemy |
| Data Processing | Pandas |
| API | REST API with OpenAPI documentation |
| Testing | Pytest |
| Deployment Setup | Docker, Docker Compose |
| Input Data | CSV |

---

## Project Architecture

```
custody-reconciliation-workbench
│
├── frontend/                 React + Vite user interface
│   └── src/
├── backend/
│   ├── app/
│   │   ├── main.py           FastAPI application and API endpoints
│   │   ├── reconciliation.py Reconciliation engine and CSV validation
│   │   ├── models.py         SQLAlchemy database models
│   │   └── database.py       Database connection
│   └── tests/                Unit tests
├── database/
│   └── schema.sql            PostgreSQL schema reference
├── sample_data/              Fictional sample CSV files
├── screenshots/              Application screenshots
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## Getting Started

### Prerequisites
- Docker Desktop / Docker Engine with Compose (recommended)
- Or, for a manual setup: Python 3.11+, Node.js 20+ and npm, PostgreSQL 16

### Run Using Docker

Clone the repository:

```bash
git clone https://github.com/tusharr-code/custody-reconciliation-workbench.git
```

Navigate to the project directory:

```bash
cd custody-reconciliation-workbench
```

Start the application:

```bash
docker compose up --build
```

Then open:

| Service | URL |
|---|---|
| Frontend | http://localhost:5173 |
| API health check | http://localhost:8000/health |
| Interactive API docs | http://localhost:8000/docs |

To stop: `docker compose down`. To reset the development database: `docker compose down -v` (deletes all local data).

Development database credentials are intentionally simple and **must** be changed before any shared or production deployment. Copy `.env.example` if you want to run the API outside Docker.

### Run Tests

```bash
cd backend
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
pytest -q
```

---

## How to Use

1. Select **Transaction** or **Position** as the reconciliation type.
2. Select the business date.
3. Upload the custodian CSV and the internal CSV (try the files in `sample_data/`).
4. Click **Load & Reconcile**.
5. Review matched records and breaks in the grids.
6. Open **Open Breaks** and click **Investigate** to assign a root cause, owner, status and comment.
7. Export break records using **Export breaks**.

### Supported Transaction Columns
`account` (or `account_id`), `transaction_id` (or `trade_id`), `security` (or `security_name` / `ticker`), `transaction_type`, `trade_date`, `settlement_date`, `quantity` (or `qty`), `price`, `net_amount` (or `amount`), `currency`.

Default matching: account + transaction ID, with quantity tolerance 0.000001, amount tolerance 0.01, price tolerance 0.0001, and exact currency and dates.

### Supported Position Columns
`account`, `security` (or `security_name` / `ticker`), `currency`, `quantity` (or `qty`), `market_value` (or `value`), `price`.

Default matching: account + security + currency, with quantity tolerance 0.000001 and market value tolerance 0.01.

---

## Business Use Cases

This project explores reconciliation workflows relevant to:

- Custodian versus internal accounting reconciliation.
- Fund accounting operations.
- Investment operations.
- Cash and position reconciliation.
- Financial data quality monitoring.
- Break investigation and exception management.

---

## Future Enhancements

- Advanced one-to-many and many-to-one transaction matching.
- Corporate action reconciliation.
- User authentication and role-based access control.
- Maker-checker approval workflow.
- Tamper-evident audit trail with user identity.
- Advanced reconciliation dashboards and analytics.
- Detailed position history search interface.
- Scheduled reconciliation and automated notifications.
- Integration with external custodian data feeds.

---

## About the Developer

I have 7.5+ years of experience in financial markets and investment operations, with practical exposure to reconciliation processes and exception investigation.

This project reflects my interest in combining financial domain expertise with software development, data analytics and automation to solve practical challenges in financial operations.

**Areas of Interest:**
- Custody and Fund Accounting
- Investment Operations
- Financial Data Analytics
- Reconciliation Automation
- FinTech and Product Data Engineering

**Connect with me:**
- GitHub: https://github.com/tusharr-code
- LinkedIn: https://www.linkedin.com/in/tushar-ramugade-3abbb915b

---

## Disclaimer

This is a portfolio and learning project intended to demonstrate reconciliation concepts and application development. All sample data is fictional.

It is not a production-ready financial reconciliation system. Production deployment would require additional security controls, authentication, auditability, operational resilience, data governance and comprehensive integration testing.

If you find this project interesting, feel free to explore the repository, share feedback or connect for collaboration.
