# OpenMetadata GitHub Repository — Workflow Directory Map

Source reviewed: `open-metadata/OpenMetadata` on GitHub, main branch, checked April 28, 2026.

## Purpose of this file

This file is a directory-first learning guide for the OpenMetadata GitHub repository. 

It does **not** attempt to explain every file yet. Instead, it identifies the major directories that are part of the OpenMetadata workflow and explains what each directory is for.


## High-level OpenMetadata workflow

OpenMetadata has four major workflow concepts:

1. **Metadata definitions** — entity schemas, request/response models, and metadata vocabulary.
2. **Metadata ingestion** — connectors and workflows that collect metadata from external systems.
3. **Metadata service/API** — backend service that stores, exposes, secures, and manages metadata.
4. **User interface** — frontend experience for discovery, governance, lineage, quality, and collaboration.

A simplified workflow looks like this:

```text
External Data Systems
        |
        v
ingestion/
        |
        v
openmetadata-service/
        |
        v
Metadata Store + APIs
        |
        v
openmetadata-ui/
```

Supporting directories such as `docker/`, `openmetadata-airflow-apis/`, `openmetadata-clients/`, `openmetadata-sdk/`, and `openmetadata-integration-tests/` support deployment, orchestration, client access, and validation.

---

## Repository root directories reviewed

The GitHub repository root currently includes these major directories:

```text
OpenMetadata/
├── .agents/
├── .claude/
├── .devcontainer/
├── .github/
├── bin/
├── bootstrap/
├── common/
├── conf/
├── docker/
├── docs/
├── examples/
├── ingestion/
├── openmetadata-airflow-apis/
├── openmetadata-clients/
├── openmetadata-dist/
├── openmetadata-integration-tests/
├── openmetadata-k8s-operator/
├── openmetadata-mcp/
├── openmetadata-sdk/
├── openmetadata-service/
├── openmetadata-shaded-deps/
├── openmetadata-spec/
├── openmetadata-ui-core-components/
├── openmetadata-ui/
├── openspec/
├── scripts/
└── skills/
```

---

## Directory groups by workflow role

### 1. Core workflow directories

These are the main directories to study first because they explain how OpenMetadata actually works.

| Directory | Workflow role | Why it matters |
|---|---|---|
| `ingestion/` | Metadata collection workflow | Contains the ingestion framework, connectors, pipelines, plugins, and workflow execution logic. |
| `openmetadata-spec/` | Metadata model/specification | Contains the metadata entity specifications used to define OpenMetadata’s domain model. |
| `openmetadata-service/` | Backend/API service | Contains the Java backend service that exposes APIs, manages entities, security, resources, and persistence. |
| `openmetadata-ui/` | User-facing application | Contains the UI application that users interact with for discovery, lineage, governance, quality, and collaboration. |
| `docker/` | Local deployment/runtime | Contains Docker Compose and runtime configuration used to run OpenMetadata locally or in development. |

---

### 2. Orchestration and integration directories

These support workflow execution, external orchestration, and programmatic access.

| Directory | Workflow role | Why it matters |
|---|---|---|
| `openmetadata-airflow-apis/` | Airflow-managed ingestion workflows | Provides an Airflow plugin/API layer for deploying OpenMetadata workflow definitions and managing DAGs/tasks. |
| `openmetadata-clients/` | Generated or packaged clients | Contains client libraries, including Java client support, for communicating with OpenMetadata APIs. |
| `openmetadata-sdk/` | SDK access layer | Provides a Java SDK with fluent APIs for entity operations such as tables, users, search, lineage, and governance entities. |
| `examples/` | Usage examples | Contains examples, including Python SDK and data-quality examples, useful after the core workflow is understood. |

---

### 3. Deployment and platform directories

These are useful after understanding the core service and ingestion workflow.

| Directory | Workflow role | Why it matters |
|---|---|---|
| `openmetadata-dist/` | Distribution/package assembly | Supports packaging and distribution of OpenMetadata components. |
| `openmetadata-k8s-operator/` | Kubernetes operator | Supports Kubernetes-based management and deployment workflows. |
| `bootstrap/` | Bootstrapping/setup support | Helps initialize or prepare runtime/development setup. |
| `conf/` | Configuration | Contains configuration used by services or deployment workflows. |
| `bin/` | Executable scripts | Contains command-line helper scripts. |
| `scripts/` | Build/dev automation | Contains automation scripts for build, generation, validation, or development support. |

---

### 4. Testing and validation directories

These are important for understanding how OpenMetadata validates changes.

| Directory | Workflow role | Why it matters |
|---|---|---|
| `openmetadata-integration-tests/` | Integration testing | Contains tests that validate how OpenMetadata components work together. |
| `ingestion/tests/` | Ingestion-specific tests | Validates ingestion connectors, workflows, and pipeline behavior. |
| `.github/` | CI/CD workflows | Contains GitHub Actions and repository automation used for validation and release workflows. |

---

### 5. UI and shared component directories

These matter when studying the frontend workflow.

| Directory | Workflow role | Why it matters |
|---|---|---|
| `openmetadata-ui/` | Main frontend application | Main user interface source. |
| `openmetadata-ui-core-components/` | Shared UI components | Reusable UI building blocks used across the frontend. |

---

### 6. Documentation, standards, and supporting directories

These are helpful references but are not usually the first workflow directories to study.

| Directory | Workflow role | Why it matters |
|---|---|---|
| `docs/` | Documentation support | Repository documentation source/support. |
| `openspec/` | Specification support | Supports OpenMetadata specification-related work. |
| `common/` | Shared common code | Shared utilities or common definitions used by other modules. |
| `openmetadata-shaded-deps/` | Dependency packaging | Handles shaded Java dependencies. |
| `openmetadata-mcp/` | MCP-related support | Supports Model Context Protocol-related functionality. |
| `.devcontainer/` | Dev container setup | Development environment configuration. |
| `.agents/`, `.claude/`, `skills/` | AI/agent support | Contributor/developer assistance files; not central to the metadata workflow. |

---

## Recommended learning order

Use this order to understand the OpenMetadata workflow from source system to user interface.

### Step 1 — `ingestion/`

Start here because ingestion explains how OpenMetadata pulls metadata from external systems.

Focus areas:

```text
ingestion/
├── examples/
├── operators/
├── pipelines/
├── plugins/
├── src/
└── tests/
```

Takeaway:

`ingestion/` is where metadata collection begins. This is where connectors and workflow logic gather metadata from databases, dashboards, pipelines, messaging systems, storage systems, and other sources.

---

### Step 2 — `openmetadata-spec/`

Study this next because it defines what metadata means inside OpenMetadata.

Focus areas:

```text
openmetadata-spec/
└── src/
```

Takeaway:

`openmetadata-spec/` defines the schema and model layer. This is the contract that tells OpenMetadata what entities such as tables, dashboards, pipelines, users, tags, domains, policies, and data products look like.

---

### Step 3 — `openmetadata-service/`

Study this after the specification layer because this is the backend that uses those models.

Focus areas:

```text
openmetadata-service/
└── src/
```

Takeaway:

`openmetadata-service/` is the central backend. It exposes APIs, handles entity resources, manages security, stores metadata, and serves the UI and clients.

---

### Step 4 — `openmetadata-ui/`

Study this after the backend because the UI is the consumer of the service APIs.

Focus areas:

```text
openmetadata-ui/
└── src/main/resources/ui/
```

Takeaway:

`openmetadata-ui/` is where users interact with the metadata graph through discovery pages, lineage views, governance features, quality results, collaboration tools, and administration screens.

---

### Step 5 — `docker/`

Study this after the main application flow because Docker shows how the pieces are run together.

Focus areas:

```text
docker/
├── development/
├── docker-compose-ingestion/
├── docker-compose-openmetadata/
├── docker-compose-quickstart/
├── mysql/
├── postgresql/
├── rdf-store/
├── openmetadata-start.sh
├── openmetadata.yaml
└── run_local_docker.sh
```

Takeaway:

`docker/` explains the runtime environment. It shows how OpenMetadata, its database, search dependencies, ingestion services, and optional supporting services are launched locally.

---

### Step 6 — `openmetadata-airflow-apis/`

Study this after ingestion and Docker because it explains scheduled/orchestrated ingestion.

Focus areas:

```text
openmetadata-airflow-apis/
├── development/airflow/
├── examples/
├── openmetadata_managed_apis/
└── tests/
```

Takeaway:

`openmetadata-airflow-apis/` connects OpenMetadata ingestion workflows with Airflow. It helps deploy workflow definitions and manage DAGs/tasks from Airflow.

---

### Step 7 — `openmetadata-clients/` and `openmetadata-sdk/`

Study these after the backend API because they show how external code talks to OpenMetadata.

Focus areas:

```text
openmetadata-clients/
└── openmetadata-java-client/

openmetadata-sdk/
└── src/
```

Takeaway:

These directories are for programmatic access. They show how applications, scripts, or services can interact with OpenMetadata without directly writing raw REST calls every time.

---

### Step 8 — `openmetadata-integration-tests/`

Study this after the workflow is clear because tests show expected behavior.

Takeaway:

`openmetadata-integration-tests/` helps verify that ingestion, APIs, services, and supporting components work together correctly.

---

## Directory-first workflow map

```text
1. External system exists
   Example: Postgres, Snowflake, MySQL, Kafka, Looker, Airflow, S3

2. ingestion/ connects to the external system
   It extracts metadata, profiles, lineage, usage, and quality-related information.

3. openmetadata-spec/ defines the shape of the metadata
   The metadata must match OpenMetadata entity models and request schemas.

4. openmetadata-service/ receives and manages the metadata
   It exposes APIs, persists metadata, applies security, and manages relationships.

5. openmetadata-ui/ displays the metadata to users
   Users search, document, govern, review lineage, inspect quality, and collaborate.

6. docker/ supports local runtime
   It runs OpenMetadata and dependencies for development or proof-of-concept work.

7. openmetadata-airflow-apis/ supports scheduled ingestion
   Airflow can run and manage ingestion workflows.

8. clients/sdk/tests support integration and validation
   External tools can call OpenMetadata APIs, and tests confirm the system works.
```

---

## First directory to review

Start with:

```text
ingestion/
```

Reason:

This is the best starting point because it shows how metadata enters OpenMetadata. Once ingestion is clear, the rest of the workflow becomes easier to understand:

```text
ingestion -> specification -> service/API -> UI -> deployment/orchestration
```

---

## Next step

When ready, review **Procedure 1: `ingestion/` workflow**.

