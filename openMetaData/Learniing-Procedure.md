Below is a suggested set of step‑by‑step procedures for reviewing the various workflow-related directories in the OpenMetadata repository.  

Each procedure focuses on a specific “workflow” folder.

⸻

## Procedure 1 – Ingestion Workflows (Python)

Location: 
> ingestion/src/metadata/workflow  

This directory contains the Python code that defines and orchestrates ingestion workflows (e.g. application workflows, data quality workflows).

1. Navigate to the directory in your local checkout: cd ingestion/src/metadata/workflow.
2. Open the README.md first—it gives a high‑level overview of how ingestion workflows are structured.
3. Inspect base.py to understand the base Workflow class.  Note how it handles initialization, context management, and execution.
4. Read application.py and data_quality.py to see concrete workflow implementations.  These files show how different workflow types subclass the base class.
5. Explore the context/ subfolder to see how workflow context is built and passed between tasks.  Focus on files like context.py and any helper modules.

⸻

## Procedure 2 – Example Ingestion Workflow Configurations

Location: 
> ingestion/src/metadata/examples/workflows  

This folder holds sample YAML files that show how to configure ingestion workflows for different sources (Airflow, Athena, etc.).

1. Navigate to the examples directory.
2. List the YAML files and notice the naming pattern (e.g. athena.yaml, airbyte.yaml).
3. Pick a couple of YAML files to open—look for the source, sink, and workflowConfig sections to see how they map to the ingestion code.
4. Note any common fields across the examples (service name, connection details, schedule, filters) and how they relate to your own environment.


⸻

## Procedure 3 – Server‑Side Workflow Handlers (Java)

Locations:

> openmetadata-service/src/main/java/org/openmetadata/service/workflows/ 
 
> openmetadata-service/src/main/java/org/openmetadata/service/governance/workflows/

These Java packages define workflow interfaces and handlers used by the OpenMetadata server.

1. Start with the workflows/interfaces package to see any generic interfaces.
2. In the governance/workflows package, open WorkflowHandler.java and Workflow.java.  These classes describe how workflows are registered, executed and monitored on the server side.
3. Browse related classes such as WorkflowEventConsumer.java or WorkflowFailureListener.java to understand how events and failures are handled.
4. Pay attention to annotations or configuration hooks that tie back to the JSON definitions described in Procedure 4.

⸻

## Procedure 4 – Governance Workflow Definitions (JSON Data)

Location: 
> openmetadata-service/src/main/resources/json/data/governance/workflows

This directory contains ready‑to‑load JSON workflow definitions used for governance tasks (approvals, reviews, incidents, etc.).

1. List all the JSON files; their names indicate the workflow purpose (e.g. DataAccessRequestTaskWorkflow.json, GenericIncidentTaskWorkflow.json).
2. Open one of the JSON files.  Examine the displayName, tasks, transitions, and trigger fields to see how a workflow is declared.
3. Compare a few definitions to see how tasks and transitions vary by workflow type.
4. Note how these JSON files are loaded by the Java classes from Procedure 3.

⸻

## Procedure 5 – Workflow Schema Definitions

Locations:

> openmetadata-spec/src/main/resources/json/schema/governance/workflows

> openmetadata-spec/src/main/java/org/openmetadata/schema/governance/workflows

These folders hold the formal schema and Java classes that describe workflow structures.

1. In the JSON schema folder, open workflow.json (or similarly named files) to understand the allowed fields and validation rules for workflows.
2. In the Java folder, open classes that mirror the schema definitions (often auto‑generated).  Observe how fields are mapped and annotated.
3. Check how these classes are used elsewhere in the codebase (e.g. referenced by the server).

⸻

## Procedure 6 – Airflow‑Managed API Workflows (Python)

Location: 
> openmetadata-airflow-apis/openmetadata_managed_apis/workflows

Here you’ll find Python helpers for building and executing workflows via OpenMetadata’s Airflow‑managed APIs.

1. Open workflow_factory.py and workflow_builder.py to see how managed workflows are constructed for Airflow execution.
2. Inspect the ingestion/ subfolder to see specific ingestion workflows built on top of the factory.
3. Note how configuration files or parameters map to Airflow DAGs.

Once you understand how Airflow integration works, we can move on.

⸻

## Procedure 7 – GitHub and CI Workflows

Location: 
> .github/workflows (and skills/.github/workflows)

These are YAML files for CI/CD actions and automation tasks.

1. Browse the workflow names (ci.yml, release.yml, etc.) to understand what tasks run in the GitHub pipeline.
2. Open one or two of these YAML files to see how tests, linters, or deployments are orchestrated.
3. Recognize that these GitHub workflows are infrastructure automation rather than metadata ingestion or governance.

After reviewing these, let me know if you’d like to explore any additional workflow directories (e.g. test workflows or UI localization). Otherwise we can start executing the procedures one by one.
