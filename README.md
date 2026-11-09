# Study Progress Analysis (SPA) – Full-Stack System Hub

[![Stage: Beta](https://img.shields.io/badge/Stage-Beta%20v0.4.0-blue.svg)](docs/wiki/Releases.md)
[![License](https://img.shields.io/badge/Academic-SSE%20Uni--Hildesheim-green.svg)](https://www.uni-hildesheim.de/sse/)
[![Stack](https://img.shields.io/badge/Stack-React%2018%20%7C%20FastAPI%20%7C%20PostgreSQL%20%7C%20Docker-informational.svg)](docs/wiki/Architecture.md)
[![Tests: Passing](https://img.shields.io/badge/Live%20Tests-11%2F11%20Passing-success.svg)](test_all_userstories_live.py)

Welcome to the central repository for the **Study Progress Analysis (SPA)** platform, developed for **Stiftung Universität Hildesheim (Software Systems Engineering - SSE)**.

The SPA platform enables university lecturers, examination offices, and academic staff to ingest heterogeneous exam spreadsheets (`.xlsx`, `.csv`, `.tsv`, `.ods`), review and validate student marks with in-flight editing, track longitudinal academic trajectories across semesters, manage course documents via the Course Drive, compare exam sittings side-by-side, and evaluate student success metrics.

This umbrella repository orchestrates the complete multi-tier system, linking the decoupled frontend and backend services via Git submodules and Docker Compose.

---

## 🏛️ System Architecture & Submodules

The system is decoupled into independent, containerized services:

| Component | Repository & Technology | Description |
| :--- | :--- | :--- |
| **Frontend Client** | [**`d2-project-client`**](https://github.com/poalelungi-ion/d2-project-client)<br>`React 18`, `TypeScript 5`, `Vite`, `AG Grid`, `Material-UI`, `Zustand` | Single-page application providing spreadsheet ingestion wizard, AG Grid inline reviewer, Course Drive vault, and interactive analytics. |
| **Backend Service** | [**`d2-project-backend`**](https://github.com/poalelungi-ion/d2-project-backend)<br>`Python 3.11+`, `FastAPI`, `SQLAlchemy 2.0`, `Pydantic`, `Alembic` | REST API layer enforcing ACID transaction safety, dynamic column mapping, study program alias normalization, and JWT auth. |
| **Database** | `PostgreSQL 15`<br>`Alpine Linux container` | Relational database storing students, courses, exam sittings, and historical mark trajectories. |
| **Orchestrator** | `Docker Compose`<br>`docker-compose.yml` | Unified multi-container orchestration with zero-rebuild runtime environment injection. |

---

## ⚡ Quickstart: Running with Docker Compose

### Prerequisites
- [Docker Engine](https://docs.docker.com/engine/install/) & Docker Compose (v2.20+)
- Git

### 1. Clone with Submodules
```bash
git clone --recurse-submodules https://github.com/poalelungi-ion/study-progress-analysis.git
cd study-progress-analysis
```

*(If cloned without submodules, initialize them via: `git submodule update --init --recursive`)*

### 2. Configure Environment
```bash
cp .env.example .env
```

The default `.env` is pre-configured for instant local development:
```env
VITE_API_BASE_URL=http://localhost:8000/api
CORS_ORIGINS=http://localhost:5173,http://127.0.0.1:5173
POSTGRES_USER=spa_user
POSTGRES_PASSWORD=spa_password
POSTGRES_DB=spa_db
```

### 3. Build & Launch the Application Stack
```bash
docker compose up -d --build
```

### 4. Access the Live Services
- 🌐 **Frontend Application:** [http://localhost:5173](http://localhost:5173)
- 📖 **Backend Swagger / OpenAPI Docs:** [http://localhost:8000/docs](http://localhost:8000/docs)
- 🗄️ **PostgreSQL Database:** `localhost:5432` (`spa_user` / `spa_password` / `spa_db`)

---

## 🧪 Live Evaluation Suite

An automated live verification suite evaluates all core user stories against the active Docker stack:

```bash
python test_all_userstories_live.py
```

### Verified User Stories & Capabilities:
- ✅ **Strict Column Standardization (#99906):** Validates required German academic headers (`Matrikelnummer`, `Fach`, `Studiengang`, `Versuch`, `Bewertung`).
- ✅ **Numeric Grade Enforcement (#104084):** Restricts grades strictly to numerical `1.0`–`5.0`.
- ✅ **Dynamic Review & Inline Editing (#104089, #97743):** Interactive AG Grid preview allowing column remapping and in-flight typo fixes.
- ✅ **Study Program Alias Normalization (#104102):** Resolves acronyms (e.g. `M.Sc. WINF` → `Wirtschaftsinformatik (Master of Science)`) and cleans float `.0` IDs.
- ✅ **Free-Form Exam Attempt Field (#104109):** Custom sittings (e.g., "Klausur 1", "Wiederholungsprüfung").
- ✅ **Consolidated Best Mark Column (#104098):** Real-time computation of highest grade per student.
- ✅ **Chronological Mark History (#104104):** Detailed modal showing student grade trajectory.
- ✅ **Course Marks Table Viewport Stability (MR !70):** Zero-collapse flex layout across single and comparative exam modes.
- ✅ **Dedicated Course Drive Tab (#104092, #104090):** Standalone document vault decoupled from file ingestion.

---

## 📚 Master Documentation & Specifications

Complete technical specifications and academic deliverables are preserved in [`docs/`](docs/):

1. **System & Requirements Documentation:**
   - 📄 **[Requirements Specification PDF](docs/specifications/D2_SOSE_26-Study Progress Analysis.pdf):** Original SSE project problem description and requirements catalog.
   - 📊 **[UML Diagrams](docs/uml/):** Class diagrams, sequence charts, and domain models.
   - 📋 **[Requirements Management](docs/requirements/):** Backlog definitions, acceptance criteria, and user story catalogs.
   - 📝 **[Meeting Notes](docs/meeting-notes/):** Sprint reviews, retrospectives, and client alignment logs.

2. **Technical Wiki (`docs/wiki/`):**
   - **[System Architecture](docs/wiki/Architecture.md):** Complete component topology and data flows.
   - **[Delimited Releases Log](docs/wiki/Releases.md):** Release changelog from Sprint 0 (`v0.0.1-alpha`) to Sprint 4 (`v0.4.0-beta`).
   - **[Traceability Matrix](docs/wiki/Traceability-Matrix.md):** Bidirectional requirements-to-code mapping.
   - **[Sprint 4 Deliverables](docs/wiki/sprints/Sprint-4.md):** Production Ingestion & Course Marks Milestone.

---

## 👥 Core Project Team (Group D2)

| Name | Role | Email |
| :--- | :--- | :--- |
| **Ion Poalelungi** | Architecture & Frontend Lead | `poalelungi@uni-hildesheim.de` |
| **Anna Chiriciuc** | Frontend & Quality Assurance | `chiriciuc@uni-hildesheim.de` |
| **Sudarshan Bashyal** | Backend Lead & Security | `sudarshan.bashyal@uni-hildesheim.de` |
| **Yazan Al Rifaee** | Full-Stack Developer | `alrifaee@uni-hildesheim.de` |
| **Marvin Wucher** | Full-Stack Developer | `wucher@uni-hildesheim.de` |
| **Amara Aslam** | Frontend Developer | `aslam@uni-hildesheim.de` |
| **Aditi Joshi** | QA & Frontend Developer | `joshi@uni-hildesheim.de` |
