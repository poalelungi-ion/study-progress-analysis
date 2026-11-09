# Software Architecture & UML Specifications

This document outlines the high-level system architecture and data models for the SPA (Study Progress Analysis) System.

## 1. High-Level Architecture (C4 Context)

The system follows a standard modern web application architecture isolated via Docker containers.

```mermaid
graph TD
    Teacher[Teacher / Administrator]
    
    subgraph Docker Host
        Frontend[React Vite SPA Frontend \n Port: 5173]
        Backend[FastAPI Backend Server \n Port: 8000]
        Database[(PostgreSQL Database \n Volume: postgres_data)]
        Storage[Local File Storage \n Volume: ./backend/uploaded_excels]
    end

    Teacher -->|Interacts with UI| Frontend
    Teacher -->|Uploads LSF Excels| Frontend
    Frontend -->|REST API Calls| Backend
    Backend -->|SQLAlchemy ORM| Database
    Backend -->|Saves Raw Backup| Storage
```

## 2. Entity Relationship Diagram (ERD)

The database strictly models the many-to-many relationship between Students and Courses through the intermediate `ExamResult` and `Exam` entities.

```mermaid
erDiagram
    STUDENT {
        int student_id PK
        string name
        string program
        string status
    }
    
    COURSE {
        int course_id PK
        string course_name
        boolean is_archived
    }
    
    EXAM {
        int exam_id PK
        int course_id FK
        string semester
    }

    EXAM_RESULT {
        int result_id PK
        int student_id FK
        int exam_id FK
        float grade
        boolean passed
    }

    COURSE ||--o{ EXAM : "has many"
    EXAM ||--o{ EXAM_RESULT : "has many"
    STUDENT ||--o{ EXAM_RESULT : "completes"
```

## 3. Upload & Thesis Data Flow (Sequence Diagram)

This sequence demonstrates the core business logic of data ingestion, including the fallback saving mechanic to ensure persistency.

```mermaid
sequenceDiagram
    actor User as Teacher
    participant UI as React Frontend
    participant API as FastAPI Backend
    participant FS as Host File System
    participant DB as PostgreSQL

    User->>UI: Selects .xlsx file & Semester
    UI->>API: POST /api/upload/ (multipart/form-data)
    
    API->>FS: os.makedirs() & write(contents)
    FS-->>API: File safely stored in /uploaded_excels
    
    API->>API: pandas.read_excel(contents)
    API->>DB: Start Database Transaction (db.begin())
    
    loop For each row in Excel
        API->>DB: Check if Course exists (with_for_update)
        API->>DB: Check if Exam exists for Semester
        API->>DB: Upsert ExamResult (Keep lowest numeric grade)
    end
    
    DB-->>API: Commit Transaction
    API-->>UI: Return 200 OK & Preview Data
    UI-->>User: Display Toast Success Message
```

## 4. Technology Stack

- **Frontend:** React 18, Vite, Material-UI (MUI), AG Grid (for data tables), Recharts (for dashboards).
- **Backend:** Python 3.10+, FastAPI, SQLAlchemy, Pandas (for ETL / ingestion), Uvicorn.
- **Database:** PostgreSQL 15.
- **Infrastructure:** Docker, Docker Compose (3 containers linked via bridge network).
