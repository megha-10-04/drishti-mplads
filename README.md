# Drishti — AI-Powered MPLADS Monitoring & Audit Prioritisation

An explainable, data-driven decision-support system that helps prioritise public infrastructure projects for human review by identifying cost anomalies, delivery risks, duplicate records, and unusual spending concentrations.

Drishti is designed to work with real MPLADS records. It processes imported datasets, generates evidence-backed risk indicators, and presents findings through an API-driven dashboard. It does not fabricate records or treat risk indicators as proof of fraud.

## Overview

Public infrastructure monitoring involves large volumes of project and expenditure data. Reviewing every record manually can be time-consuming.

Drishti helps make this process more focused by:

- Identifying projects with unusual expected costs.
- Highlighting potential delivery delays and stalled works.
- Detecting potentially duplicated project records.
- Analysing spending concentration across agencies.
- Maintaining data provenance and officer-review history.
- Providing explainable signals to support human decision-making.

## Key Features

- **Real-data processing:** Import CSV and JSON datasets with automatic column mapping and validation.
- **Cost anomaly detection:** Compare project costs against expected costs based on available project characteristics.
- **Delivery-risk analysis:** Estimate delivery risk when sufficient labelled historical data is available.
- **Duplicate detection:** Identify potentially duplicated records using multiple corroborating attributes.
- **Spending concentration analysis:** Compare agency-level spending patterns against broader trends.
- **Data quality reporting:** Identify missing, invalid, or inconsistent source data.
- **Review history:** Preserve record provenance and officer-review decisions.
- **Interactive dashboard:** Explore analytical results through a React frontend connected to a REST API.

## Tech Stack

| Layer | Technologies |
|---|---|
| Frontend | React, Vite, JavaScript |
| Backend | Python, FastAPI |
| Data processing | Pandas, CSV/JSON validation |
| Machine learning | Regression, logistic classification, anomaly scoring |
| Database | SQLite, PostgreSQL |
| API | REST |
| Deployment | Docker, Docker Compose |
| Testing | Pytest |

## System Architecture

```text
Official Data Sources
        |
        v
 CSV / JSON Import
        |
        v
 Column Mapping & Validation
        |
        v
 Data Quality Reporting
        |
        v
 Analytics & Risk Engine
        |
        v
 Database + Provenance
        |
        v
 FastAPI REST API
        |
        v
 React Dashboard
        |
        v
 Human Review & Prioritisation
```

## Analytics Approach

### Cost Anomaly Detection
Estimates expected project costs using available project attributes such as project type, district, year, and size. Unusual residuals are flagged for further investigation.

### Delivery-Risk Estimation
Uses historical project outcomes and pre-outcome features to estimate delivery risk. The model remains unavailable when there is insufficient labelled history rather than reporting unsupported performance metrics.

### Duplicate Record Detection
Combines evidence such as project descriptions, agencies, amounts, and dates to identify records that may refer to the same work.

### Spending Concentration
Examines agency-level spending shares relative to their broader spending patterns to highlight unusual concentrations.

**Important:** These outputs are investigation priorities, not fraud verdicts. Final decisions require human review and verification.

## Getting Started

### Prerequisites

- Python 3.10 or a compatible version supported by the dependencies
- Node.js and npm
- Git

### 1. Clone the repository

```bash
git clone https://github.com/megha-10-04/drishti-mplads.git
cd drishti-mplads
```

### 2. Start the backend

```bash
cd backend
pip install -r requirements.txt
uvicorn app:app --reload
```

The API should be available at `http://localhost:8000`.

### 3. Start the frontend

Open a second terminal:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL printed by Vite, usually `http://localhost:5173`.

### 4. Import data

Open the dashboard and navigate to the data-import section. Import a compatible CSV or JSON dataset to populate the analytics.

A sample fixture is available at:

`backend/tests/fixtures/esakshi_sample.csv`

The sample fixture is intended for testing, not as evidence of real-world model performance.

## Connecting Data Sources

Drishti supports importing official exports and includes a connector for the data.gov.in API, which requires a valid API key and the appropriate resource ID.

A live e-SAKSHI API integration has not been verified. Official exports can be imported instead.

For configuration details, see `.env.example` and the backend connector modules.

## Testing

Run the backend tests:

```bash
cd backend
python -m pytest tests/ -q
```

## Current Limitations

- Model quality depends on the completeness and reliability of the imported data.
- Reliable delivery-risk estimation requires sufficient labelled historical records.
- Live e-SAKSHI API access is not currently verified.
- Map-based analysis requires geographic coordinates in the source data.
- Role-based access control requires production-grade authentication and authorisation before deployment in a real operational environment.

## Responsible Use

Drishti is a decision-support tool. Its outputs are designed to help reviewers prioritise records for investigation, not to automatically establish misconduct or fraud. Data quality, explainability, provenance, and human oversight are central to its intended use.

## Author

**Megha Kakkar**

GitHub: [@megha-10-04](https://github.com/megha-10-04)

---

*Built to make public infrastructure monitoring more transparent, explainable, and data-driven.*
