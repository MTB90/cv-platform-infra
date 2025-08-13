# Project Architecture

### High-Level Overview:

This section outlines the high-level architecture of the system, where each major component is defined and its
interaction with other components is described. The architecture revolves around a **FastAPI** backend, **Argo Workflow
** for background processing, **CrewAI** for agent-based task execution, and various storage systems.

```
                    
                                                                            Client
                                                                             ▲ 
                                                                             │  │     upload file
                                                                http         │  │ pre-signed-url (http)
                                                        ┌────────────────────┘  └──────────────────────┐ 
                                                        │                                              │  
                                                        ▼                                              │  
                                                 ┌────────────────┐                                    │  
      ┌────────────────┐                         │    (api/v1)    │                                    ▼
      │  Argo Workflow │                         │--------------- │     generate pre-signed-url    ┌─────────┐
      │                │ <─────── k8s req ───────│  cv-platform   │ <──── minio async client ────> │  MinIO  │
      └────────────────┘                         │    backend     │                                │         │
            │                                    │                │                                │         │
            │                                    │                │                                │         │
            │                            ┌─────> │                │                                │         │
            │                            │       │----------------│      events put,delete         │         │
            │                            │       │  (api/private) │ <----------------------------- │         │
            │                            │       └────────────────┘                                └─────────┘
            │                            │                                                              ▲
            │                            │       ┌──────────────┐                                       │
            │                            └─────> │  PostgreSQL  │                                       │
            │                                    │ (Persistent) │                                       │
            │                                    └──────────────┘                                       │
            │                                                                                           │
            │                                                                                           │ 
            ▼                                                                                           │             
       ┌────────────┐                                                                                   │
       │  Workflow  │<──────────────────────────────────────────────────────────────────────────────────┘                                  
       │------------│                            
       │   CrewAI   │
       └────────────┘                          
```

### Task Flow:

1. **Client**:
    - The client sends an HTTP request to **FastAPI**, and also uploads document using presigned url to minio.


2. **Backend (FastAPI)**:
    - FastAPI triggers the Argo Workflow using hera client: https://hera.readthedocs.io/en/stable/


3. **Argo Workflow**:
    - Create new specific Workflow for uploaded document:
        - Get document from Minio
        - Transform/Create new document using AI - CrewAI
        - Store new document in Minio


4. **Notification**:
    - Events (put, delete) on any document is send back to Backend

---
