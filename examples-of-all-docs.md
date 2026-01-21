# Example Reference Sheet (Mocked Data)

## SPA-PAM — Single-Page Application: Pet Adoption Marketplace

### Document Set Index (Final Sequence)

1. Project Charter
2. Stakeholder Communication Plan
3. Risk Management Plan & Risk Register
4. Software Requirements Specification (SRS)
5. Architecture Contract Specification (ACS)
6. Software Design Document (SDD / SAD)
7. Change Management Plan & Change Requests
8. Test Plan
9. Deployment / Release Plan
10. Project Closure / Post-Implementation Report

---

## Document 1 — Project Charter (Mocked Example)

**Project Name:** SPA-PAM (Pet Adoption Marketplace)
**Date:** November 2025
**Sponsor:** Lopez Family Solutions
**PM:** Larry Lopez
**Version History:** v1.0 initial, v1.1 favorites/messaging, v1.2 AWS deployment scope

**Objectives (SMART):**

* Breeder listings CRUD by Dec 2025
* Favorites by Dec 2025
* Messaging by Jan 2026
* AWS deployment by Jan 2026
* Full document suite delivered by Jan 2026

**In-Scope:** Auth (JWT/RBAC), listings, S3 images, favorites, messaging, admin oversight, AWS hosting
**Out-of-Scope:** Payments, native mobile, push notifications

---

## Document 2 — Stakeholder Communication Plan (Mocked Example)

### Communication Objectives

* Weekly visibility into progress, risks, and decisions
* Same-day escalation for blockers impacting schedule or security

### Stakeholder List

* Sponsor (Lopez Family Solutions)
* PM/PO (Larry Lopez)
* Engineering (Larry Lopez)
* QA (Larry Lopez)
* Ops/DevOps (Larry Lopez)
* Users (Breeders, Customers, Admin)

### Communication Matrix (Sample)

| Audience           | Information                    | Frequency     | Channel            | Owner |
| ------------------ | ------------------------------ | ------------- | ------------------ | ----- |
| Sponsor            | Status, risks, major decisions | Weekly        | Email summary      | PM    |
| Sponsor            | Go/No-Go for release           | Per release   | Email + short call | PM    |
| Users (test group) | UAT instructions, known issues | Per UAT cycle | Email or doc link  | PM    |
| Internal team      | Daily progress/blockers        | Daily         | Task board notes   | PM    |

### Escalation Rules (Sample)

* Security issue or data leak risk: escalate same day to Sponsor
* Missed milestone risk: escalate within 24 hours

---

## Document 3 — Risk Management Plan & Risk Register (Mocked Example)

### Scoring Model

* Probability: Low/Med/High
* Impact: Low/Med/High
* Exposure: qualitative based on combined rating

### Risk Register (Sample)

| Risk ID | Description                                      | Category    | Prob | Impact | Response                              | Owner | Status     |
| ------- | ------------------------------------------------ | ----------- | ---- | ------ | ------------------------------------- | ----- | ---------- |
| R-001   | AWS S3/CloudFront misconfig causes broken assets | Technical   | Med  | High   | Mitigate: staged deploy + checklist   | Larry | Open       |
| R-002   | MongoDB Atlas M0 throughput limits slow tests    | Operational | High | Med    | Mitigate: test data limits + off-peak | Larry | Open       |
| R-003   | CORS errors block image upload                   | Technical   | Med  | High   | Mitigate: signed URL pattern          | Larry | Mitigating |
| R-004   | Scope creep (payments) delays release            | Business    | Med  | High   | Avoid: explicitly out-of-scope        | Larry | Controlled |

---

## Document 4 — Software Requirements Specification (SRS) (Mocked Example)

### Requirement Samples

* **FR-01:** Breeder shall create a dog listing with required fields (name, breed, ageMonths, sex). Priority: High. Related Risks: R-002, R-003
* **FR-02:** Unauthenticated users shall browse dogs with filters. Priority: High. Related Risks: R-002
* **FR-03:** Customers shall add/remove favorites by dogId. Priority: Medium.
* **NFR-01 Performance:** 95% of GET /dogs responses under 300ms in normal load. Related Risks: R-002
* **NFR-02 Security:** Authenticated endpoints require JWT bearer token; role enforcement required. Related Risks: R-001

---

## Document 5 — Architecture Contract Specification (ACS) (Mocked Example)

### Contract Anchors

* Public schemas: Dog, User, Message
* Error contract: `{ "error": "...", "code": "..." }`
* Security boundary: JWT + RBAC, HTTPS required
* SLOs: latency, availability, error rate
* Versioning: `/api/v1`, breaking changes -> `/api/v2`

### Acceptance Criteria (Sample Status)

| Requirement                   | Status                   |
| ----------------------------- | ------------------------ |
| APIs implemented per contract | Complete                 |
| Schemas validated             | Complete                 |
| RBAC enforced                 | Complete                 |
| Error contract consistent     | Complete                 |
| SLOs tested                   | Partial (needs perf run) |

---

## Document 6 — Software Design Document (SDD / SAD) (Mocked Example)

### Architecture Style

* React SPA frontend
* Node/Express layered backend
* MongoDB Atlas
* S3 signed URLs for images
* CloudFront for static distribution

### Key Design Decisions (Sample)

* Use public UUIDs (`dogId`, `userId`) to avoid leaking database IDs
* Keep S3 object keys internal; expose only signed URLs (aligns with ACS)
* Index dogs collection on `breed`, `sex`, `location` to support browsing performance

### Traceability Example

* FR-01 -> Dog Module -> POST /api/dogs internal flow -> ACS schema Dog Create -> tests TC-API-POST-DOG-01

---

## Document 7 — Change Management Plan & Change Requests (Mocked Example)

### Change Categories

* Minor: internal refactor, no contract change
* Major: impacts SRS/ACS/SDD or release scope
* Emergency: production safety fix

### Change Log (Sample)

| CR ID  | Title                                      | Affected Docs                     | Decision | Date       | Notes                     |
| ------ | ------------------------------------------ | --------------------------------- | -------- | ---------- | ------------------------- |
| CR-001 | Add favorites feature                      | Charter, SRS, ACS, SDD, Test Plan | Approved | 2025-12-02 | Added endpoints + schemas |
| CR-002 | Switch backend deploy target to App Runner | SDD, Deployment Plan              | Approved | 2026-01-04 | Reduced ops overhead      |
| CR-003 | Add payments                               | Charter, SRS, ACS                 | Deferred | 2026-01-06 | Out-of-scope for MVP      |

### Change Request (CR) Snapshot (Example)

* **CR ID:** CR-002
* **Description:** Deploy backend via App Runner instead of EC2 for predictable releases
* **Impact:** Schedule improves, ops risk reduced
* **Risks:** Updates R-001 mitigation approach
* **Decision:** Approved

---

## Document 8 — Test Plan (Mocked Example)

### Entry Criteria (Sample)

* SRS baseline approved
* ACS baseline approved
* Staging environment available
* Seed test users created

### Exit Criteria (Sample)

* No Critical/High defects open
* ACS acceptance checks pass
* UAT sign-off complete

### Test Items (Sample)

* Auth, Listings CRUD, Favorites, Messaging, Admin moderation, S3 image upload, RBAC enforcement

---

## Document 9 — Deployment / Release Plan (Mocked Example)

### Strategy

* Staging deploy -> smoke tests -> promote -> frontend deploy -> CloudFront invalidation

### Smoke Tests (Sample)

* Login (all roles)
* Create listing (breeder)
* Browse/filter listings (public)
* Favorites add/remove (customer)
* Send message (customer -> breeder)
* Images load via signed URLs

### Rollback Triggers (Sample)

* Authentication failures
* Schema mismatch vs ACS
* Sustained 500 errors
* Broken static assets after deploy

---

## Document 10 — Project Closure / Post-Implementation Report (Mocked Example)

### Objectives vs Outcomes (Sample)

* Listings CRUD: Met
* Favorites: Met
* Messaging: Met
* AWS deployment: Met
* Payments: Not met (deferred)

### Residual Risks (Sample)

* R-002 MongoDB M0 throughput remains a scaling constraint; accepted for MVP

### Transition

* Ops owner: Larry Lopez
* Runbooks: Deployment plan + environment notes
* Support: Self-supported (single developer)

