# SAP-Sentinel-AI
AI-powered inventory risk monitoring and anomaly investigation using Python, SAP HANA Cloud, Gemini, and Streamlit.

The application combines Python-based risk analysis, SAP HANA Cloud data storage, a Streamlit dashboard, and Google's Gemini API to help users investigate inventory shortages and unusual stock movements.

Project status: Working prototype. Inventory and stock-movement demo data are stored in SAP HANA Cloud. A live SAP S/4HANA business-data integration is not yet implemented.

✨ Features

Inventory risk analysis: Classifies materials using configurable reorder-point rules.
Stock coverage calculations: Estimates how long current inventory may last based on supplied daily usage.
Anomaly detection: Uses the interquartile range (IQR) method to flag unusual stock movements.
AI-assisted investigation: Uses Gemini to summarize supplied inventory evidence and suggest investigation steps.
Procedure retrieval: Retrieves relevant local inventory procedures using keyword matching.
SAP HANA Cloud integration: Reads inventory and stock-movement data through Python database access and SQL views.
Interactive dashboard: Presents inventory metrics, alerts, and investigation reports through Streamlit.
Mock data support: Allows local development without an active HANA connection when configured appropriately.
