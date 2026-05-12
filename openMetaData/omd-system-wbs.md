```markdown
OpenMetadata-PoC
├── AWS Foundation (Epic)
│   ├── Compute Platform Selection (Task)
│   │   ├── Evaluate compute models (Subtask)
│   │   │   ├── EC2 (VM-based)
│   │   │   ├── EKS (Kubernetes)
│   │   │   ├── ECS / Fargate
│   │   │   └── Hybrid approach
│   │   ├── Define workload characteristics (Subtask)
│   │   │   ├── Stateless vs stateful
│   │   │   ├── Scaling expectations
│   │   │   └── Availability requirements
│   │   └── Select final compute architecture (Subtask)
│   │
│   ├── Kubernetes / Container Orchestration (Task)
│   │   ├── Create EKS cluster (Subtask)
│   │   │   ├── Define cluster configuration
│   │   │   ├── Configure node groups
│   │   │   └── Select instance types
│   │   ├── Configure cluster networking (Subtask)
│   │   │   ├── VPC integration
│   │   │   ├── Subnets (public/private)
│   │   │   └── Security groups
│   │   ├── Deploy core services (Subtask)
│   │   │   ├── CoreDNS / kube-proxy
│   │   │   ├── Metrics server
│   │   │   └── Ingress controller (ALB / NGINX)
│   │   └── Validate cluster health (Subtask)
│   │
│   ├── Compute Resource Configuration (Task)
│   │   ├── Select instance types (Subtask)
│   │   │   ├── CPU sizing
│   │   │   ├── Memory sizing
│   │   │   └── Cost optimization (spot/on-demand)
│   │   ├── Configure autoscaling (Subtask)
│   │   │   ├── Horizontal Pod Autoscaler
│   │   │   ├── Cluster Autoscaler
│   │   │   └── Scaling policies
│   │   └── Define resource limits (Subtask)
│   │       ├── CPU limits
│   │       ├── Memory limits
│   │       └── QoS classes
│   │
│   ├── Storage & Database Infrastructure (Task)
│   │   ├── Define storage strategy (Subtask)
│   │   │   ├── EBS (block)
│   │   │   ├── S3 (object)
│   │   │   └── EFS (shared)
│   │   ├── Provision database services (Subtask)
│   │   │   ├── RDS (Postgres/MySQL)
│   │   │   ├── Backup configuration
│   │   │   └── Multi-AZ setup
│   │   ├── Configure persistence (Subtask)
│   │   │   ├── Persistent Volumes
│   │   │   └── Storage classes
│   │   └── Data lifecycle policies (Subtask)
│   │
│   ├── Networking Foundation (Task)
│   │   ├── Create VPC (Subtask)
│   │   │   ├── CIDR planning
│   │   │   ├── Public/private subnets
│   │   │   └── Route tables
│   │   ├── Configure connectivity (Subtask)
│   │   │   ├── Internet Gateway
│   │   │   ├── NAT Gateway
│   │   │   └── VPC endpoints
│   │   ├── Define security controls (Subtask)
│   │   │   ├── Security Groups
│   │   │   ├── NACLs
│   │   │   └── Firewall rules
│   │   └── DNS & routing (Subtask)
│   │       ├── Route 53
│   │       └── Domain setup
│   │
│   ├── Identity & Access Management (Task)
│   │   ├── Define IAM roles (Subtask)
│   │   │   ├── EKS roles
│   │   │   ├── EC2 roles
│   │   │   └── Application roles
│   │   ├── Configure least privilege (Subtask)
│   │   └── Enable authentication (Subtask)
│   │       ├── OIDC for Kubernetes
│   │       └── SSO integration
│   │
│   ├── Observability & Monitoring (Task)
│   │   ├── Logging setup (Subtask)
│   │   │   ├── CloudWatch logs
│   │   │   ├── Container logs
│   │   │   └── Application logs
│   │   ├── Metrics collection (Subtask)
│   │   │   ├── CPU/memory
│   │   │   ├── Kubernetes metrics
│   │   │   └── Custom metrics
│   │   ├── Alerting (Subtask)
│   │   └── Dashboard setup (Subtask)
│   │
│   ├── Security & Compliance Baseline (Task)
│   │   ├── Enable encryption (Subtask)
│   │   │   ├── At rest (EBS/RDS)
│   │   │   └── In transit (TLS)
│   │   ├── Configure secrets management (Subtask)
│   │   │   ├── AWS Secrets Manager
│   │   │   └── Kubernetes secrets
│   │   ├── Enable audit logging (Subtask)
│   │   │   ├── CloudTrail
│   │   │   └── Kubernetes audit logs
│   │   └── Map to NIST 800-53 controls (Subtask)
│   │
│   └── CI/CD & Deployment Pipeline (Task)
│       ├── Setup container registry (Subtask)
│       │   ├── ECR repository
│       │   └── Image versioning
│       ├── Configure build pipeline (Subtask)
│       │   ├── GitLab / GitHub Actions
│       │   └── Build + test stages
│       ├── Deployment automation (Subtask)
│       │   ├── Helm charts
│       │   └── Kubernetes manifests
│       └── Validate deployment workflow (Subtask)
│
├── Infrastructure Platform (Epic)
│   ├── Deploy OpenMetadata Stack (Task)
│   │   ├── Setup Docker Compose / Helm (K8s)   
│   │   ├── Configure OpenMetadata service
│   │   └── Configure dependencies (Elasticsearch, Airflow, MySQL)
│   ├── Setup Database Layer (Task)
│   │   ├── Create databases
│   │   ├── Seed data
│   │   └── Define schemas
│   └── Configure Networking (Task)
│       ├── Setup ports / ingress
│       ├── Validate UI access
│       └── Configure service connectivity
│
├── Metadata Ingestion System (Epic)
│   ├── Define Data Sources (Task)
│   │   ├── Identify systems
│   │   └── Define ingestion scope
│   ├── Build Ingestion Pipelines (Task)
│   │   ├── Create configs
│   │   ├── Schedule ingestion
│   │   └── Validate runs
│   └── Validate Metadata (Task)
│       ├── Verify schemas
│       ├── Check lineage
│       └── Validate extraction
│
├── Governance System (Epic)
│   ├── Define Policies (Task)
│   │   ├── Access control rules
│   │   ├── Role mapping
│   │   └── Compliance alignment
│   ├── Implement Metadata Governance (Task)
│   │   ├── Tagging
│   │   ├── Ownership
│   │   └── Classification
│   └── Data Quality Integration (Task)
│       ├── Define checks
│       ├── Integrate Great Expectations
│       └── Store results
│
├── Data Contracts System (Epic)
│   ├── Define Contracts (Task)
│   │   ├── Schema definitions
│   │   ├── Constraints
│   │   └── Ownership metadata
│   ├── Build Validation Engine (Task)
│   │   ├── Python scripts
│   │   ├── Enforcement logic
│   │   └── Error handling
│   └── CI/CD Integration (Task)
│       ├── Trigger validation
│       ├── Fail on violations
│       └── Publish results
│
├── Orchestration System (Dagster) (Epic)
│   ├── Setup Dagster (Task)
│   │   ├── Initialize repo
│   │   ├── Configure jobs
│   │   └── Setup resources
│   ├── Build ETL Pipelines (Task)
│   │   ├── Extract
│   │   ├── Transform
│   │   └── Load
│   └── Metadata Sync (Task)
│       ├── Trigger ingestion
│       ├── Push lineage
│       └── Sync catalog
│
├── Observability & Lineage (Epic)
│   ├── Enable Lineage (Task)
│   │   ├── Configure sources
│   │   ├── Validate lineage
│   │   └── Map transformations
│   ├── Monitoring & Alerts (Task)
│   │   ├── Setup alerts
│   │   ├── Monitor jobs
│   │   └── Track quality
│   └── Logging (Task)
│       ├── Capture logs
│       ├── Store metadata
│       └── Analyze failures
│
├── User Experience & Validation (Epic)
│   ├── UI Exploration (Task)
│   │   ├── Search datasets
│   │   ├── View schemas
│   │   └── Explore lineage
│   ├── Role Testing (Task)
│   │   ├── Validate permissions
│   │   ├── Test workflows
│   │   └── Confirm governance
│   └── Feedback Loop (Task)
│       ├── Collect feedback
│       ├── Identify issues
│       └── Refine configs
│
└── Documentation & Evaluation (Epic)
    ├── Documentation (Task)
    │   ├── Architecture diagrams
    │   ├── Setup guides
    │   └── Config documentation
    ├── Evaluation (Task)
    │   ├── Measure success
    │   ├── Identify gaps
    │   └── Assess adoption
    └── Roadmap Planning (Task)
        ├── Define production architecture
        ├── Plan scaling
        └── Define next steps
```