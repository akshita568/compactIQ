# CompactIQ Enterprise Compliance Engine

> **Hackathon Project Overview:**  
> **CompactIQ** is an automated compliance and dependency mapping engine designed to bridge the gap between static enterprise vendor documentation (such as release notes and compatibility matrices) and live endpoint telemetry. By combining an AI-powered document ingestion pipeline with a local system agent, CompactIQ dynamically builds a knowledge graph that instantly identifies hardware and software compatibility conflicts across enterprise desktop environments.

---

## 🚀 Features

- AI-powered compatibility document ingestion
- Automated dependency and rule extraction using Gemini
- Live endpoint hardware & software inventory scanning
- Interactive knowledge graph visualization
- Enterprise compliance validation
-  Admin dashboard for rule management
- Cross-platform Electron desktop application

---

# Architecture

```
                    ┌────────────────────────────┐
                    │ Compatibility PDFs         │
                    │ Release Notes              │
                    │ Vendor Documentation       │
                    └────────────┬───────────────┘
                                 │
                                 ▼
                    ┌────────────────────────────┐
                    │ Gemini AI                  │
                    │ Document Parsing           │
                    │ Rule Extraction            │
                    └────────────┬───────────────┘
                                 │
                                 ▼
                    ┌────────────────────────────┐
                    │ FastAPI Backend            │
                    │ SQLAlchemy                 │
                    │ Compliance Engine          │
                    └────────────┬───────────────┘
                                 │
                ┌────────────────┴────────────────┐
                ▼                                 ▼
     ┌─────────────────────┐           ┌──────────────────────┐
     │ SQLite/PostgreSQL   │           │ Electron Desktop App │
     │ Knowledge Base      │           │ React Frontend       │
     └─────────────────────┘           └──────────┬───────────┘
                                                  │
                                                  ▼
                                   ┌──────────────────────────┐
                                   │ Local System Agent       │
                                   │ Hardware Scan            │
                                   │ Software Inventory       │
                                   └──────────────────────────┘
```

---

# Tech Stack

### Backend

- FastAPI
- SQLAlchemy
- SQLite / PostgreSQL
- Google GenAI SDK (Gemini 2.0 Flash)
- Pydantic
- PyMuPDF

### Desktop Application

- Electron
- React
- React Router (HashRouter)
- Tailwind CSS
- Glassmorphism UI

### System Scanning

- Node.js
- Electron IPC
- PowerShell Integration

---

# Prerequisites

Ensure the following software is installed before running the project.

- Python **3.10+**
- Node.js
- npm
- Git
- Gemini API Key

---

# Backend Setup

## 1. Clone the Repository

```bash
git clone https://github.com/yourusername/CompactIQ.git

cd CompactIQ
```

---

## 2. Create a Virtual Environment

### Windows (PowerShell)

```powershell
python -m venv venv

.\venv\Scripts\activate
```

### macOS / Linux

```bash
python3 -m venv venv

source venv/bin/activate
```

---

## 3. Install Python Dependencies

```bash
pip install -r requirements.txt
```

If required, install manually:

```bash
pip install fastapi
pip install uvicorn
pip install sqlalchemy
pip install aiosqlite
pip install pydantic-settings
pip install google-genai
pip install aiofiles
pip install python-multipart
pip install pymupdf
```

---

## 4. Configure Environment Variables

Inside the backend directory copy the example environment file.

### Windows

```powershell
cp .env.example .env
```

### Linux/macOS

```bash
cp .env.example .env
```

Update the `.env` file:

```env
GEMINI_API_KEY=your_api_key_here

USE_SQLITE=true

ADMIN_MAINTENANCE_PASSWORD=admin123
```

### Environment Variables

| Variable | Description |
|----------|-------------|
| `GEMINI_API_KEY` | Required for AI document parsing |
| `USE_SQLITE` | Set `true` for local development |
| `ADMIN_MAINTENANCE_PASSWORD` | Password used for admin maintenance actions |

---

## 5. Run the Backend

```bash
python -m uvicorn app.main:app --reload --port 8000
```

Backend URL:

```
http://localhost:8000
```

Swagger Documentation:

```
http://localhost:8000/docs
```

---

# 🖥️ Desktop Application Setup

Navigate into the frontend directory.

```bash
cd frontend
```

Install dependencies.

```bash
npm install
```

---

## Launch the Electron Desktop App

Ensure the FastAPI backend is already running.

Then execute:

```bash
npm run electron-dev
```

This command will:

- Start the React development server
- Launch Electron
- Connect Electron to the FastAPI backend
- Enable local system scanning

---

# Project Workflow

## Client / Endpoint Agent

When the application launches:

1. Electron invokes the local system agent.
2. Hardware information is collected.
3. Installed software inventory is generated.
4. Inventory is sent to the backend.
5. Components are matched against extracted compliance rules.
6. Compatibility conflicts are displayed.
7. Interactive dependency graph is generated.

---

## Admin Dashboard

Switch roles using the **Change Role** button.

Available modules include:

### Document Ingestion

Upload compatibility PDFs from:

```
Testing_docs/
└── compatibility_docs/
```

Gemini automatically extracts:

- Product versions
- Hardware requirements
- Software dependencies
- Compatibility constraints
- Upgrade rules

---

### Rules Matrix

View all extracted:

- Dependencies
- Version constraints
- Compatibility rules
- Relationships

---

### Knowledge Base Administration

Admin tools include:

- Database cleanup
- Rule maintenance
- Knowledge base reset
- Record management

---

### Knowledge Graph

Switch back to the Client role to visualize:

- Installed software
- Hardware components
- Dependency relationships
- Compatibility paths
- Rule mappings

---

# Application Flow

```
Upload PDF
      │
      ▼
Gemini AI extracts rules
      │
      ▼
Rules stored in Database
      │
      ▼
Electron scans local machine
      │
      ▼
Inventory sent to Backend
      │
      ▼
Compliance Engine
      │
      ▼
Conflict Detection
      │
      ▼
Knowledge Graph Visualization
```

---

# Suggested Project Structure

```
CompactIQ
│
├── app/
│   ├── api/
│   ├── models/
│   ├── services/
│   ├── routes/
│   ├── database/
│   └── main.py
│
├── frontend/
│   ├── src/
│   ├── electron/
│   ├── public/
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

## Zero Rules Extracted

Possible causes:

- Invalid Gemini API key
- Incorrect model name
- Empty PDF
- Parsing failure

Verify:

```env
GEMINI_API_KEY=your_api_key
```

Ensure the project references:

```
gemini-2.0-flash
```

---

## 404 Errors During Ingestion

Check:

- Backend is running
- Correct API endpoints
- Uploaded file format
- Route configuration

---

## Frontend Cannot Connect to Backend

Verify:

Backend is running on

```
http://localhost:8000
```

Launch the application using:

```bash
npm run electron-dev
```

rather than opening the React app directly in a browser.

---

## Electron System Scan Fails

Check:

- PowerShell execution permissions
- Node.js installation
- Electron IPC handlers
- Local scanning scripts

---

# Future Enhancements

- Active Directory integration
- Multi-endpoint enterprise monitoring
- Real-time compliance alerts
- Vendor-specific rule packs
- Automatic remediation suggestions
- Cloud-hosted compliance engine
- Policy versioning
- Historical compatibility tracking

---

# Contributors

Built as a hackathon project to demonstrate how AI-powered document intelligence and endpoint telemetry can be combined to automate enterprise software and hardware compatibility analysis.

---

## License

This project is intended for educational and hackathon purposes.