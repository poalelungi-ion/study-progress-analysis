# Change Management & Versioning Log

This document provides a trace of all major architectural and feature-level changes made to the system. Future maintainers should update this document before pushing to production to ensure complete historical traceability.

## Version 1.0.0 (MVP Release) - Current

**Date:** July 2026
**Theme:** Initial Architecture, Ingestion Engine, and Hildesheim UI Alignment.

### 1. Database & Backend Adjustments
- **Feature:** Implemented PostgreSQL containerization.
- **Change:** Removed testing `Base.metadata.drop_all()` call to ensure data is strictly persisted across container rebuilds.
- **Traceability:** Fulfills requirement for resilient local deployment. 
- **Persistence Extension:** Added `os.makedirs` and write functionality to `/api/upload/` to physically save backup `.xlsx` and `.csv` files onto the host machine via Docker Volume mounts.

### 2. Analytical Engine
- **Feature:** Added Pandas processing to securely parse and clean messy LSF data.
- **Change:** Implemented a unique Thesis grading endpoint (`/api/upload/thesis/`) that calculates a weighted (27 + 3) average and automatically rounds to the closest legitimate German grade increment.
- **Change:** Migrated Dashboard calculations to compute "Program Pass Rates" (e.g. M.Sc. SE) rather than faculty abstractions, matching actual provided data shapes.

### 3. UI / UX Overhaul
- **Feature:** Integrated Material-UI and Recharts.
- **Change:** Switched from generic blue wireframe to the official "University of Hildesheim" red (`#c8102E` -> `#B71C1C`) and white minimalist aesthetic. 
- **Change:** Removed all "Avatar" and "Student Photo" instances to maintain GDPR compliance and a professional, data-centric interface. Reduced global font weights from `800/900` blocks to sleeker `500/700` metrics.
- **Change:** Injected gradient cell styling in AG Grid (Green 1.0 -> Red 5.0) for immediate visual identification of struggling grades.

### 4. Deprecations
- **Feature Removed:** Email alert logic and "At Risk" messaging.
- **Reason:** Stakeholders clarified the application functions strictly as a data-analysis tool with no student-facing user management.

---

## Instructions for Future Developers

When implementing new features requested by stakeholders:
1. Document the requirement in `traceability_matrix.md` with a new `REQ-` identifier.
2. If changing database models or flow, update the Mermaid diagrams in `architecture_and_uml.md`.
3. Log the successful implementation in this file with the next sequential Version number.
