# Requirements Traceability Matrix (RTM)

This document maps the initial stakeholder requirements (from meeting notes) through Agile Epics/User Stories down to the actual Software Specifications (Codebase). This ensures every implemented feature directly aligns with a requested business need.

## 1. Core Data Ingestion & Grading Logic

| Req ID | Source (Meeting Notes) | Agile Epic / User Story | Software Specification (Code Implementation) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **REQ-1.1** | *24.06.2026:* "Upload Excel/CSV grades extracted from LSF directly into the system." | **Epic 3:** Data Ingestion<br>US 3.1: Support Excel/CSV file processing. | `backend/main.py` -> `@app.post("/api/upload/")`<br>Uses `pandas` for multi-format ingestion. | ✅ Implemented |
| **REQ-1.2** | *Re-elicitation:* "Users want to be able to just copy-paste raw CSV data directly instead of saving files." | **Epic 3:** Data Ingestion<br>US 3.2: Raw text ingestion endpoint. | `backend/main.py` -> `@app.post("/api/upload/raw/")`<br>`frontend/src/App.jsx` -> `handleRawCsvSubmit()` | ✅ Implemented |
| **REQ-1.3** | *01.07.2026:* "Master Thesis requires 2 supervisors: Written grade (27 ECTS) + Oral Grade (3 ECTS). Aggregate into single exam grade." | **Epic 4:** Grading Logic<br>US 4.1: Weighted average thesis calculator. | `backend/main.py` -> `@app.post("/api/upload/thesis/")`<br>Applies `(27*W + 3*O)/30` and snaps to closest valid grade increment. | ✅ Implemented |
| **REQ-1.4** | *24.06.2026:* "Student grades must be standard German increments (1.0, 1.3, 1.7... 4.0, 5.0)." | **Epic 4:** Grading Logic<br>US 4.2: Grade increment validation. | `backend/main.py` -> `valid_grades = [1.0, 1.3, 1.7... 5.0]`<br>Used in thesis rounding and frontend validation. | ✅ Implemented |

## 2. Analytics & Dashboard

| Req ID | Source (Meeting Notes) | Agile Epic / User Story | Software Specification (Code Implementation) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **REQ-2.1** | *24.06.2026:* "Visual rendering of pass rates, average grades, and total students." | **Epic 6:** Analytics & Dashboards<br>US 6.1: High-level KPI Dashboard. | `backend/main.py` -> `@app.get("/api/stats/")`<br>`frontend/src/App.jsx` -> `renderDashboard()` mapping KPIs. | ✅ Implemented |
| **REQ-2.2** | *01.07.2026:* "Show grade distribution across 1.0 to 5.0, and qualitative metrics (Excellent/Fail)." | **Epic 6:** Analytics & Dashboards<br>US 6.2: Grade visualization charts. | `frontend/src/App.jsx` -> Uses `recharts` for Grade Distribution BarChart and Qualitative BarChart. | ✅ Implemented |
| **REQ-2.3** | *Re-elicitation:* "Pass rates should be broken down by Study Program (M.Sc. IMIT, SE), not by generalized faculties." | **Epic 6:** Analytics & Dashboards<br>US 6.3: Program-specific pass rates. | `backend/main.py` -> `program_distribution` calculation grouping by `Student.program`. Frontend Donut chart mapping. | ✅ Implemented |
| **REQ-2.4** | *01.07.2026:* "Dashboard should match the University of Hildesheim styling (Red #c8102E header, professional)." | **Epic 2:** SPA Desktop UI<br>US 2.1: Unified UI/UX Styling. | `frontend/src/App.jsx` -> Global `ThemeProvider` setting primary color `#B71C1C` (Red). Minimalist white backgrounds. | ✅ Implemented |
| **REQ-2.5** | *Re-elicitation:* "Color gradients in tables: 1.0 is green, 5.0 is red." | **Epic 2:** SPA Desktop UI<br>US 2.2: Roster Gradients. | `frontend/src/App.jsx` -> `gradeCellStyle` function computing dynamic `rgba()` values based on `params.value`. | ✅ Implemented |

## 3. Operations & Persistence

| Req ID | Source (Meeting Notes) | Agile Epic / User Story | Software Specification (Code Implementation) | Status |
| :--- | :--- | :--- | :--- | :--- |
| **REQ-3.1** | *24.06.2026:* "Export all data to Excel and provide Archive downloads." | **Epic 7:** Exporting<br>US 7.1: Excel & JSON archiving. | `backend/main.py` -> `@app.get("/api/export/excel")` using `io.BytesIO`. | ✅ Implemented |
| **REQ-3.2** | *Re-elicitation:* "System must survive Docker container rebuilds. Save uploaded Excels safely." | **Epic 1:** Data Architecture<br>US 1.2: Persistent Data Volumes. | `docker-compose.yml` -> `postgres_data` volume.<br>`backend/main.py` -> Writes to `uploaded_excels/` which maps to host volume. | ✅ Implemented |
| **REQ-3.3** | *01.07.2026:* "No automated email alerts for students. No student accounts or user management." | **Epic 1:** Data Architecture<br>US 1.3: Anonymous/Teacher-only operation. | Removed `send_email` logic. Application functions entirely autonomously via LSF metrics. | ✅ Implemented |
