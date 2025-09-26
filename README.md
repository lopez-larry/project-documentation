project-documentation

flowchart TD

    A[Project Charter / Initiation Document] --> B[Software Requirements Specification (SRS)]
    B --> C[Software Design Document (SDD/SAD)]
    C --> D[Test Plan]
    D --> E[Deployment / Release Plan]
    E --> F[Project Closure / Post-Implementation Report]

    classDef start fill:#f9f,stroke:#333,stroke-width:2px;
    classDef doc fill:#bbf,stroke:#333,stroke-width:1px;
    classDef end fill:#bfb,stroke:#333,stroke-width:2px;

    A:::start
    B:::doc
    C:::doc
    D:::doc
    E:::doc
    F:::end
