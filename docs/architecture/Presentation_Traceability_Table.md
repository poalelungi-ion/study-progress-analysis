# SPA System Traceability Matrix (Presentation Format)

| ID | Ass. ID | Requirements Description | Business Need, Justification | Project Objective | Requested By | Department | WBS Element | Specification | Design | Test Cases |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **1** | 1.1 | **Excel Data Ingestion** | Teachers need a way to upload raw LSF grades effortlessly | Automate data processing | Stakeholders | Academic Admin | 1.1 | In Progress | In Progress | 1001, 1002 |
| **1** | 1.2 | **Master Thesis Logic** | Thesis requires complex 27+3 ECTS weighting into a single grade | Accurate final grade calculation | Academic Board | Academic Admin | 1.2 | In Progress | In Progress | 1003 |
| **2** | 2.1 | **Visual Analytics Dashboard** | Fast visualization of pass rates & grade distributions | Provide Data Insights | Teachers | Faculty | 2.1 | In Progress | In Progress | 2001 |
| **2** | 2.2 | **Roster Color Gradients** | Immediate visual cues for struggling vs excelling students (1.0 to 5.0) | Enhance UI/UX | Teachers | Faculty | 2.2 | In Progress | In Progress | 2002 |
| **3** | 3.1 | **No User Accounts** | GDPR compliance, autonomous operation without student logins | Secure Architecture | Stakeholders | IT Security | 3.1 | In Progress | In Progress | 3001 |
| **3** | 3.2 | **Data Persistence** | Uploaded Excel files must survive server/container rebuilds | System Resilience | IT Admin | IT Infrastructure | 3.2 | In Progress | In Progress | 3002 |
| **4** | 4.1 | **Raw CSV Paste Upload** | Fallback for users unable to format Excel files | User Accessibility | Teachers | Faculty | 4.1 | In Progress | In Progress | 4001 |
| **4** | 4.2 | **Archive Export** | Need ability to backup full system state to JSON/Excel | Data Portability | Stakeholders | Academic Admin | 4.2 | In Progress | In Progress | 4002 |
| **5** | 5.1 | **Containerization Setup** | Isolate application environments for reproducible deployments | Standardize Deployment | IT Admin | DevOps | 5.1 | In Progress | In Progress | 5001 |
| **5** | 5.2 | **Automated CI/CD Pipeline** | Automate code testing and deployment to cloud servers via Jenkins | Delivery Efficiency | DevOps Team | DevOps | 5.2 | Not Started | Not Started | 5002 |
| **6** | 6.1 | **User Documentation** | Provide a manual for teachers on how to upload and analyze data | User Onboarding | Stakeholders | Training | 6.1 | In Progress | In Progress | 6001 |
| **6** | 6.2 | **System Architecture Specs** | Detail UML and database ERD for future developers | Maintainability | Project Lead | Engineering | 6.2 | In Progress | In Progress | 6002 |
