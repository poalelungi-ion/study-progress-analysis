# Study Progress Analysis (SPA) System
## Project Presentation

---

### 1. Project Overview
**Goal:** Automate and visualize student grading data from the University's LSF system.
**Target Audience:** Teachers, Administrators, and Academic Supervisors.
**Key Value Proposition:** Transforms raw, messy Excel exports into clear, actionable dashboards without requiring any manual data manipulation.

---

### 2. Core Features
- **Intelligent Data Ingestion:** Upload messy `.xlsx` or `.csv` files; the system automatically cleans data, handles missing values, and ignores non-grade codes (like "AT" or "NE").
- **Specialized Thesis Grading:** Custom logic to aggregate a Master Thesis' written grade (27 ECTS) and oral grade (3 ECTS) into a single, valid German grade increment.
- **Visual Analytics Dashboard:** Instantly view Pass Rates, Average Grades, Grade Distributions (1.0 to 5.0), and Program-specific metrics.
- **Data Export & Archiving:** Full capabilities to export cleaned data back to Excel or dump the entire database to a JSON archive.

---

### 3. Technology Stack & Architecture
- **Frontend:** React + Vite (for a lightning-fast Single Page Application), styled with Material-UI and Recharts.
- **Backend:** Python + FastAPI (for high-performance REST APIs) and Pandas (for data wrangling).
- **Database:** PostgreSQL (for robust, ACID-compliant relational data storage).
- **Deployment:** Docker & Docker Compose (for containerized, reproducible environments).
*(Note: Jenkins is not currently integrated, as the project does not yet utilize an automated CI/CD pipeline).*

---

### 4. Stakeholder Alignment & Security
- **No User Management:** As requested, the system functions autonomously without requiring student logins or tracking emails.
- **Data Persistence:** Uploaded files and database records are strictly preserved on the host machine, surviving system reboots or Docker rebuilds.
- **Hildesheim Branding:** The UI is styled cleanly with the University of Hildesheim's signature red and minimalist design.

---

### 5. Future Roadmap
- Integration with external university Identity Providers (if required later).
- Expansion of CI/CD using Jenkins to automate testing and deployments.
- Advanced predictive analytics for student success rates over multiple semesters.
