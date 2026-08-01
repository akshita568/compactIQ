# CompactIQ Enterprise Compliance Engine

CompactIQ is an enterprise-grade, AI-powered compliance engine that automates endpoint compatibility validation by combining **Generative AI**, **Knowledge Graphs**, and **live endpoint telemetry**.

Enterprise IT teams rely on release notes, compatibility matrices, firmware advisories, and security bulletins to maintain compliant systems. Since these documents are unstructured and frequently updated, manually maintaining compatibility rules is slow and error-prone.

CompactIQ solves this by allowing administrators to upload vendor documentation directly into the platform. Using **Google Gemini**, the system automatically extracts hardware requirements, software dependencies, firmware constraints, and compatibility relationships, storing them as an intelligent knowledge graph. The Electron desktop client simultaneously performs a local endpoint scan and validates the machine against the generated compliance rules, instantly identifying dependency conflicts and compatibility issues.

---

# Features

- AI-powered PDF compatibility document ingestion
- Automatic rule extraction using Google Gemini
- Knowledge Graph-based dependency mapping
- Zero-touch endpoint hardware & software scanning
- Interactive compliance dashboard
- Visual dependency graph
- Enterprise compliance validation
- Admin portal for document and rule management

---

# Architecture

The system is divided into three independent layers:

### AI Knowledge Layer
- PDF Parsing
- Google Gemini Integration
- Rule Extraction Engine
- Knowledge Graph Generation

### Compliance Engine
- FastAPI
- SQLAlchemy
- SQLite (PostgreSQL-ready)
- NetworkX Graph Engine

### Client Layer
- Electron
- React
- React Router
- Tailwind CSS
- PowerShell-based System Scanner

---

# Tech Stack

### Backend
- FastAPI
- SQLAlchemy
- SQLite / PostgreSQL
- Google GenAI SDK (Gemini 2.0 Flash)
- NetworkX
- PyMuPDF

### Frontend
- Electron
- React
- React Router (HashRouter)
- Tailwind CSS
- React Flow
- Recharts

### System Scanning
- Node.js
- Electron IPC
- Native PowerShell

---

# How It Works

1. Upload enterprise compatibility PDFs through the Admin Portal.
2. Gemini parses and extracts dependency rules.
3. Rules are stored as a knowledge graph.
4. The Electron client performs a local system scan.
5. Hardware and software inventory is sent to the backend.
6. The compliance engine validates the endpoint against extracted rules.
7. Results are displayed through dashboards and an interactive knowledge graph.

---

# Prerequisites

Before running the project, ensure the following are installed:

- Python **3.10+**
- Node.js & npm
- Git
- A valid Gemini API Key

---

# Backend Setup

## 1. Clone the Repository

```bash
git clone https://github.com/yourusername/CompactIQ.git
cd CompactIQ
```

## 2. Create a Virtual Environment

### Windows

```powershell
python -m venv venv
.\venv\Scripts\activate
```

### macOS/Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

Or manually install:

```bash
pip install fastapi uvicorn sqlalchemy aiosqlite pydantic-settings google-genai aiofiles python-multipart pymupdf networkx
```

## 4. Configure Environment Variables

Copy the example environment file:

```bash
cp .env.example .env
```

Update `.env`:

```env
GEMINI_API_KEY=your_api_key
USE_SQLITE=true
ADMIN_MAINTENANCE_PASSWORD=admin123
```

| Variable | Description |
|----------|-------------|
| `GEMINI_API_KEY` | Gemini API Key used for AI document parsing |
| `USE_SQLITE` | Enable SQLite for local development |
| `ADMIN_MAINTENANCE_PASSWORD` | Password for admin maintenance actions |

## 5. Start the Backend

```bash
python -m uvicorn app.main:app --reload --port 8000
```

Backend:

```
http://localhost:8000
```

Swagger Documentation:

```
http://localhost:8000/docs
```

---

# Desktop Application

Navigate to the frontend directory.

```bash
cd frontend
```

Install dependencies.

```bash
npm install
```

Launch the desktop application.

```bash
npm run electron-dev
```

This command starts both the React development server and the Electron desktop application.

---

# Using CompactIQ

## Admin Portal

Use the **Change Role** option to switch to the Admin Dashboard.

Available modules include:

- **Document Ingestion** – Upload compatibility PDFs from `Testing_docs/compatibility_docs/`
- **Rules Matrix** – Inspect extracted compatibility rules and dependencies
- **Knowledge Base Admin** – Manage stored compliance rules
- **Database Maintenance** – Reset or clean stored records

## Client View

On launch, the Electron client automatically:

- Collects hardware information
- Detects installed software
- Sends endpoint telemetry to the backend
- Validates the system against the knowledge graph
- Displays compliance status and detected dependency conflicts

---

# Project Structure

```text
CompactIQ
├── app/
│   ├── api/
│   ├── database/
│   ├── models/
│   ├── routes/
│   ├── services/
│   └── main.py
│
├── frontend/
│   ├── electron/
│   ├── public/
│   ├── src/
│   └── package.json
│
├── Testing_docs/
│   └── compatibility_docs/
│
├── requirements.txt
├── .env.example
└── README.md
```

---

# Troubleshooting

### No Rules Extracted

- Verify your `GEMINI_API_KEY`
- Ensure `gemini-2.0-flash` is configured
- Confirm uploaded PDFs contain extractable text

### Backend Connection Issues

- Ensure FastAPI is running on port **8000**
- Launch the project using the Electron application instead of a browser

### Endpoint Scan Fails

Verify:

- Node.js installation
- PowerShell permissions
- Electron IPC handlers

---

# 🛣 Future Roadmap

- Neo4j graph database migration
- PostgreSQL multi-tenant support
- Natural-language graph querying (Text-to-Cypher)
- Real-time compliance monitoring
- Automated remediation suggestions
- Vendor-specific compliance packs
- Historical compliance tracking
- Cloud-hosted centralized management

---

# Contributors

Developed as a hackathon project showcasing how AI-powered document intelligence, knowledge graphs, and endpoint telemetry can be combined to automate enterprise hardware and software compliance validation.

---

# License

This project is intended for educational and hackathon purposes.