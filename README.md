# 🛡️ SAP Sentinel AI

### AI-Powered Inventory Risk Monitoring & Investigation

SAP Sentinel AI is a portfolio project exploring how enterprise data, rule-based inventory analytics, statistical anomaly detection, and generative AI can work together to support inventory-risk investigation.

The application combines Python-based risk analysis, SAP HANA Cloud data storage, a Streamlit dashboard, and Google's Gemini API to help users investigate inventory shortages and unusual stock movements.

> **Project status:** Working prototype. Inventory and stock-movement demo data are stored in SAP HANA Cloud. A live SAP S/4HANA business-data integration is not yet implemented.

## ✨ Features

- **Inventory risk analysis:** Classifies materials using configurable reorder-point rules.
- **Stock coverage calculations:** Estimates how long current inventory may last based on supplied daily usage.
- **Anomaly detection:** Uses the interquartile range (IQR) method to flag unusual stock movements.
- **AI-assisted investigation:** Uses Gemini to summarize supplied inventory evidence and suggest investigation steps.
- **Procedure retrieval:** Retrieves relevant local inventory procedures using keyword matching.
- **SAP HANA Cloud integration:** Reads inventory and stock-movement data through Python database access and SQL views.
- **Interactive dashboard:** Presents inventory metrics, alerts, and investigation reports through Streamlit.
- **Mock data support:** Allows local development without an active HANA connection when configured appropriately.

## 🏗️ Architecture

```text
                 ┌────────────────────────┐
                 │   Streamlit Dashboard  │
                 └────────────┬───────────┘
                              │
                 ┌────────────▼───────────┐
                 │  Inventory Risk Engine │
                 │  Python + Pandas       │
                 └────────────┬───────────┘
                              │
             ┌────────────────┴────────────────┐
             │                                 │
  ┌──────────▼──────────┐          ┌───────────▼──────────┐
  │ Anomaly Detection   │          │ Procedure Retrieval  │
  │ IQR-based analysis  │          │ Keyword matching     │
  └──────────┬──────────┘          └───────────┬──────────┘
             │                                 │
             └────────────────┬────────────────┘
                              │
                 ┌────────────▼───────────┐
                 │  Gemini Investigation │
                 │  Evidence-based prompt│
                 └────────────────────────┘

                 Data access layer
                         │
                 ┌───────▼────────┐
                 │ SAP HANA Cloud │
                 │ Inventory data │
                 │ Movement data  │
                 └────────────────┘
```

## 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application and business logic |
| Pandas | Data processing and calculations |
| Streamlit | Interactive web dashboard |
| SAP HANA Cloud | Inventory and stock-movement data storage |
| `hdbcli` | Python database connectivity |
| Google Gemini API | AI-generated investigation reports |
| `google-genai` | Gemini Python SDK |
| `python-dotenv` | Local environment configuration |

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or a compatible version supported by the dependencies
- Git
- A Google Gemini API key for AI investigations
- SAP HANA Cloud access for database mode, or a working mock-data configuration

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/sap-sentinel-ai.git
cd sap-sentinel-ai
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows:

```powershell
.venv\Scripts\Activate.ps1
```

Or use Command Prompt:

```bat
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Configure environment variables

Copy `.env.example` to `.env` and add your own credentials.

```dotenv
DATA_SOURCE=mock
GEMINI_API_KEY=your_gemini_api_key
GEMINI_MODEL=your_supported_gemini_model
```

For HANA mode, configure the endpoint, port, database user, password, schema, and view names described in `.env.example`.

**Never commit `.env` or expose API keys, passwords, or private connection details.**

### 5. Run the application

```bash
streamlit run app.py
```

Open the local URL displayed in the terminal.

## 🗄️ SAP HANA Cloud Data Model

The prototype uses a dedicated `SENTINEL` schema containing:

- `INVENTORY` — material ID, material name, quantity, reorder point, daily usage, and unit cost.
- `STOCK_MOVEMENTS` — material ID, posting date, and quantity change.
- `SENTINEL_INVENTORY_V` — inventory view used by the Python data layer.
- `SENTINEL_STOCK_MOVEMENTS_V` — movement view used by anomaly detection.

SQL scripts and reproducible seed data should be maintained in the repository so another developer can understand and recreate the demo database.

## 🤖 AI Investigation Workflow

1. Python evaluates inventory using deterministic business rules.
2. Statistical analysis flags unusual stock movements.
3. The application retrieves relevant inventory procedures.
4. Gemini receives the selected inventory evidence and procedure text.
5. Gemini generates a narrative investigation report with potential explanations and recommended checks.

The model is instructed to distinguish supplied facts from hypotheses. The prototype does not independently verify root causes or execute stock changes.

## 🔒 Security

- Keep secrets in environment variables.
- Exclude `.env`, virtual environments, and local credentials from Git.
- Prefer a dedicated read-only database account for dashboard queries.
- Never commit production data or confidential enterprise records.
- Treat generated AI recommendations as decision support requiring human review.

## 🧪 Current Limitations

- The inventory and movement records are demonstration data stored in HANA Cloud.
- Anomaly detection currently uses a simple IQR-based method.
- Procedure retrieval uses keyword matching rather than vector search.
- Gemini produces narrative reports; comprehensive automated evaluation is still planned.
- The project is not yet connected to live SAP S/4HANA inventory through a released business API.
- Automated tests, investigation auditing, authentication, and production deployment remain future improvements.

## 🗺️ Roadmap

- [ ] Historical inventory trends and stock-movement visualizations
- [ ] Improved anomaly detection and evaluation metrics
- [ ] Structured AI outputs with evidence references
- [ ] Investigation audit trail persisted in HANA
- [ ] Automated unit and integration tests
- [ ] Optional semantic retrieval using embeddings
- [ ] SAP S/4HANA integration through approved APIs
- [ ] Deployment documentation and demo walkthrough

## 👨‍💻 Author

Built as a learning and portfolio project focused on SAP development, enterprise AI, data engineering, and Python application design.

## 📄 License

This project is intended to be released under the MIT License, subject to confirming compatibility with any incorporated third-party code and assets.
