# 📄 **Document 1: Project Charter (Project Initiation Document)**

### **SPA-PAM — Single-Page Application: Pet Adoption Marketplace**

---

## **1. Project Information**

* **Project Name:** SPA-PAM (Pet Adoption Marketplace)
* **Date:** November 2025
* **Project Sponsor:** Lopez Family Solutions / DHS Apprentice Portfolio
* **Project Manager:** Larry Lopez
* **Version/Revision History:**

  * v1.0 – Initial Project Charter
  * v1.1 – Added Favorites + Messaging scope
  * v1.2 – Added AWS S3/CloudFront deployment scope

---

## **2. Purpose & Background**

**Purpose**
Develop a full-stack MERN web application enabling breeders to list dogs and customers to find, save, and inquire about available dogs.

**Background**
Breeders often lack a modern, mobile-friendly platform to centrally manage listings. Customers have difficulty verifying legitimate breeders or browsing authenticated listings. SPA-PAM aims to solve these issues with a secure, scalable, easy-to-use marketplace.

**Organizational Alignment**
Supports portfolio development for software architecture, cloud deployment, and secure system design. Demonstrates practical application of MERN, AWS, security practices, and documentation standards.

---

## **3. Objectives (SMART)**

* Allow breeders to create and manage dog listings (by Dec 2025).
* Enable customers to browse listings and save favorite dogs (Dec 2025).
* Implement secure breeder–customer messaging (Jan 2026).
* Deploy production-ready environment using AWS S3 + CloudFront + EC2/App Runner (Jan 2026).
* Deliver complete documentation (SRS, ACS, SDD, Test Plan, Deployment Plan, Closure Report).

---

## **4. Scope**

### **In-Scope**

* User roles: Customer, Breeder, Admin
* Authentication with JWT
* Dog listing CRUD
* S3 image upload + signed URL retrieval
* Favorites system
* Customer-to-Breeder messaging inbox
* Admin oversight features
* AWS cloud deployment
* API contracts + architecture contract (2.5)

### **Out-of-Scope**

* Payment processing
* Mobile native apps
* Advanced search (multi-variable filtering)
* Multi-language support
* Push notifications

---

## **5. High-Level Requirements**

* Secure login and role-based access control
* Public dog browsing with filters
* Breeder dashboard for listing management
* Customer favorites and messaging
* Admin moderation
* Image upload with secure storage (signed URL pattern)
* Responsive and mobile-friendly interface

---

## **6. Milestones & Deliverables**

| Milestone             | Target Date | Deliverable                 |
| --------------------- | ----------- | --------------------------- |
| Requirements Complete | Dec 1       | SRS Document                |
| Contract Complete     | Dec 5       | Architecture Contract (2.5) |
| Backend MVP           | Dec 10      | Auth + Dogs API             |
| Frontend MVP          | Dec 15      | User flows + UI             |
| Full Feature Build    | Jan 5       | Favorites + Messaging       |
| Deployment            | Jan 10      | AWS Cloud Release           |
| Closure               | Jan 12      | Closure Report              |

---

## **7. Assumptions & Constraints**

### **Assumptions**

* MongoDB Atlas M0 free tier will remain available.
* S3 + CloudFront used for production hosting.
* Single developer workload is manageable.

### **Constraints**

* Cost limits (free tier or low-cost AWS).
* Limited compute resources on laptop (8GB RAM).
* Time constraints (academic + apprenticeship workload).

---

## **8. Risks & Dependencies**

### **Risks**

* Incomplete requirements → delays
* AWS misconfigurations → deployment failure
* CORS issues between frontend and backend
* Token/session mismatch issues

### **Dependencies**

* AWS (S3, CloudFront, App Runner/EC2)
* MongoDB Atlas
* Browser support (Chrome, Safari)
* Node.js + React ecosystem

---

## **9. Stakeholders**

* **Sponsor:** Lopez Family Solutions
* **Product Owner:** Larry Lopez
* **Development Team:** Larry (full stack)
* **QA:** Larry
* **Operations/DevOps:** Larry
* **End Users:** Customers, Breeders, Admin

(RACI optional)

---

## **10. Approval**

| Name        | Role         | Signature | Date   |
| ----------- | ------------ | --------- | ------ |
| Larry Lopez | PM/Architect | ______    | ______ |

---

# 📄 **Document 2: Software Requirements Specification (SRS)**

### **SPA-PAM — Single-Page Application: Pet Adoption Marketplace**

---

## **1. Introduction**

### **Purpose**

Define functional and non-functional requirements for SPA-PAM.

### **Scope**

SPA-PAM enables breeders to list dogs and customers to browse, save favorites, and contact breeders.

### **Definitions**

* **Breeder:** User who lists dogs
* **Customer:** User who browses and favorites
* **Admin:** Oversight role
* **Listing:** A dog entry created by a breeder

### **References**

* Project Charter
* ACS (2.5)
* SDD, Test Plan, Deployment Plan

---

## **2. Overall Description**

### **Product Perspective**

Web application (client–server) built on MERN stack with AWS Cloud hosting.

### **Product Functions**

* Login/Register
* Breeder dog listing management
* Dog browsing with filters
* Save favorites
* Messaging
* Admin dashboard

### **User Classes**

* Customer
* Breeder
* Admin

### **Operating Environment**

* React (Frontend)
* Node.js + Express (Backend)
* MongoDB Atlas (DB)
* AWS S3 + CloudFront (Hosting)
* Chrome/Safari browsers

### **Design & Implementation Constraints**

* Must use JWT authentication
* Must store images in S3
* Must not expose internal S3 keys

### **Assumptions & Dependencies**

* Internet connectivity
* AWS services availability

---

## **3. Functional Requirements (Selected)**

### **FR-1 Dog Listing Creation**

* **Description:** Breeder can create new dog listings.
* **Priority:** High
* **Inputs:** Dog name, breed, age, sex, image
* **Outputs:** Created public listing
* **Precondition:** Breeder authenticated
* **Postcondition:** Listing appears in GET /dogs

### **FR-2 Public Dog Browsing**

* **Description:** Customers can browse/filter dogs
* **Priority:** High
* **Inputs:** Filters (breed, sex, location)
* **Outputs:** Array of Dog objects
* **Precondition:** None

### **FR-3 Favorites**

* **Description:** Customers save/remove favorite dogs
* **Priority:** Medium
* **Inputs:** dogId
* **Outputs:** Updated favorites list

### **FR-4 Messaging**

* **Description:** Customer sends message to breeder
* **Priority:** High

---

## **4. Non-Functional Requirements**

### **Performance**

* 95% of dog search responses < 300ms

### **Security**

* JWT auth
* RBAC per role

### **Usability**

* Must support desktop and mobile

### **Availability**

* 99.5% uptime target

### **Maintainability**

* Modular React components
* Layered Node architecture

---

## **5. Use Cases (One Example)**

### **UC-1: Customer Favorites Dog**

* **Actor:** Customer
* **Precondition:** Logged in
* **Main Flow:**

  1. Customer views dog
  2. Clicks save button
  3. System stores dogId in favorites
* **Postcondition:** Dog appears in favorites list

---

## **6. Data Requirements**

* ERD includes: User, Dog, Message
* Retention: Keep listings unless deleted by breeder
* Privacy: Do not expose breeder phone number publicly

---

## **7. External Interface Requirements**

* **UI:** React web components
* **APIs:** `/api/dogs`, `/api/user/favorites`, `/api/messages`
* **Software Interfaces:** AWS S3 (image storage)

---

## **8. System Architecture & Constraints**

* MERN architecture
* AWS hosting
* Docker optional

---

## **9. Appendices**

Glossary + field definitions.

---

# 📄 **Document 2.5 — Architecture Contract Specification (ACS)**

### **SPA-PAM System Boundary Contract (External Behavior Only)**

---

## **1. Purpose**

This document defines the **externally visible behavior**, **public data schemas**, and **quality guarantees** that the SPA-PAM backend must deliver to its consumers (frontend clients, admin tools, and any future partner integrations).

The Architecture Contract:

* Specifies **WHAT** the system guarantees — not HOW it is implemented.
* Creates a **stable boundary** that remains valid regardless of internal code/design changes.
* Ensures the system is **testable**, **verifiable**, **predictable**, and **safe for integration**.
* Serves as the **Definition of Done** for system delivery prior to SDD (design) and implementation.

Internal models, database schemas, algorithms, or infrastructure details **must not** appear in this document.

---

## **2. Scope**

This contract applies to:

* All **public API endpoints**
* All **public data schemas**
* Boundary-level validation rules
* Security and access-control expectations
* Error response shapes and identifiers
* Quality attributes (SLOs)
* Versioning and compatibility rules

This contract does **NOT** include:

* Internal service logic
* Database schemas or Mongoose models
* Backend exception traces
* Internal admin-only tooling not exposed via public APIs
* Deployment choices or architecture diagrams (covered in SDD)

---

## **3. Actors (External Roles)**

The contract defines expectations for the following consumers:

* **Customer** – Browses dogs, saves favorites, messages breeders
* **Breeder** – Creates and manages listings
* **Admin** – Performs moderation
* **Unauthenticated User** – Browses public listings only
* **SPA Frontend** – Primary API consumer
* **Future API Consumers** – External clients or partners (future-proofed)

---

## **4. Data Contract (External Schema Definitions)**

### *(Authoritative source of truth for all public data shapes)*

External schemas define **exactly** what fields the frontend and integrations may rely on.
Internal metadata (MongoDB IDs, timestamps, S3 keys, internal flags, etc.) must **never** leak.

---

## **4.1 Dog (Public Schema)**

### **Fields**

| Field         | Type    | Required | Description                        | Constraints             |
| ------------- | ------- | -------- | ---------------------------------- | ----------------------- |
| `dogId`       | String  | Yes      | Public stable identifier           | UUID format             |
| `name`        | String  | Yes      | Display name                       | 1–50 chars              |
| `breed`       | String  | Yes      | Breed category                     | Must match allowed list |
| `sex`         | Enum    | Yes      | Biological sex                     | `male` or `female`      |
| `ageMonths`   | Number  | Yes      | Age in months                      | ≥ 0                     |
| `imageUrl`    | String  | Optional | Time-limited signed URL            | Public access forbidden |
| `location`    | String  | Optional | General region                     | City/State format       |
| `breederName` | String  | Yes      | Display breeder name               | No PII                  |
| `available`   | Boolean | Yes      | Whether dog is listed as available | Required for search     |

### **Business Rules**

* No internal IDs, paths, or S3 keys may appear in responses.
* `dogId` must remain stable for the life of the listing.
* A dog marked unavailable must not appear in `/api/dogs` results.

---

## **4.2 User (Public Schema)**

| Field         | Type          | Required    | Description                          | Constraints                    |
| ------------- | ------------- | ----------- | ------------------------------------ | ------------------------------ |
| `userId`      | String        | Yes         | Public UUID                          | Never reveal database IDs      |
| `role`        | Enum          | Yes         | User role                            | `customer`, `breeder`, `admin` |
| `email`       | String        | Conditional | Returned only to authenticated owner | Must be validated              |
| `profileName` | String        | Optional    | Public name                          | 1–50 chars                     |
| `favorites`   | Array(String) | Optional    | List of `dogId`s                     | Only public dog IDs allowed    |

### **Visibility Rules**

* No passwords, tokens, salts, IPs, or logs may ever appear in responses.
* Admins cannot retrieve private breeder/customer data through public APIs.

---

## **4.3 Message (Public Schema)**

| Field         | Type   | Required | Description   |
| ------------- | ------ | -------- | ------------- |
| `messageId`   | String | Yes      | UUID          |
| `senderId`    | String | Yes      | Public userId |
| `recipientId` | String | Yes      | Public userId |
| `content`     | String | Yes      | Message body  |
| `sentAt`      | String | Yes      | ISO timestamp |

### **Rules**

* No internal thread or inbox metadata permitted.
* Messages must always be associated with public user IDs only.

---

## **5. API Contract (Public Operations & Behaviors)**

### *(Describes WHAT each operation does — not internal logic)*

---

## **5.1 GET `/api/dogs`**

**Purpose:** Retrieve all publicly visible dogs.
**Auth:** Not required.
**Query Parameters:** `breed`, `sex`, `location` (optional).
**Success Response:** Array of Dog Schema.
**Error Responses:**

* `400 Invalid filters`
* `500 Server Error`

---

## **5.2 POST `/api/dogs`**

**Purpose:** Breeder creates a new dog listing.
**Auth:** Required (Bearer token).
**Access Control:** Role = `breeder`.
**Request Body:** Public Dog Create Schema (no IDs, no internal metadata).
**Success Response:** Newly created dog (Dog Schema).
**Error Responses:**

* `400 Invalid input`
* `401 Unauthorized`
* `403 Forbidden`
* `409 Duplicate listing`

---

## **5.3 GET `/api/user/current_user`**

**Purpose:** Retrieve authenticated user's public profile.
**Auth:** Required.
**Response:** User Schema.
**Errors:** `401 Unauthorized`.

---

## **5.4 POST `/api/user/favorites/:dogId`**

**Purpose:** Save dog to authenticated user's favorites.
**Auth:** Required.
**Validation:**

* `dogId` must be valid public ID.
* Dog must be publicly visible.
  **Success Response:** Updated favorites list.
  **Errors:** `400`, `401`, `404`.

---

## **5.5 Messaging Endpoints**

*(Generalized contract — specific URLs defined in final OpenAPI)*

### **POST `/api/messages/send`**

**Purpose:** Customer sends a message to breeder.
**Auth:** Required.
**Request:** `recipientId`, `content`.
**Response:** Message Schema.

### **GET `/api/messages/inbox`**

**Purpose:** Retrieve user’s inbox.
**Auth:** Required.
**Response:** Array of Message Schema.

---

## **6. Error Contract**

All APIs return errors in a standardized structure:

```json
{
  "error": "Readable message",
  "code": "ERROR_IDENTIFIER"
}
```

### **Allowed Error Identifiers**

* `AUTH_REQUIRED`
* `INVALID_INPUT`
* `FORBIDDEN`
* `NOT_FOUND`
* `SERVER_ERROR`

### **Rules**

* No stack traces or internal error objects exposed.
* Validation messages must name the invalid/missing field.

---

## **7. Security Contract**

### **Authentication**

* JWT required for all user-specific and write operations.
* Format: `Authorization: Bearer <token>`.

### **Authorization (RBAC)**

* Admin: Oversight operations
* Breeder: Listing management
* Customer: Favorites + messaging
* Public: Dog browsing only

### **Transport Security**

* HTTPS required for all environments.

### **Data Security**

* Only signed URLs may expose images.
* Breeder PII (phone, address) must never appear publicly.

---

## **8. Quality Attribute Objectives (SLOs)**

| Attribute        | Objective                          | Notes                             |
| ---------------- | ---------------------------------- | --------------------------------- |
| **Latency**      | 95% of GET /dogs < 300ms           | Includes S3 signed URL generation |
| **Availability** | 99.5% uptime (monthly)             | Applies to public APIs            |
| **Reliability**  | <0.5% error rate on valid requests | Excludes user errors              |
| **Freshness**    | Listing updates visible <5s        | Cache invalidation requirement    |
| **Scalability**  | Linear growth with traffic         | Horizontal scalable architecture  |

---

## **9. Versioning & Compatibility Strategy**

* All endpoints use prefix `/api/v1`.
* Backward-compatible additions allowed (new optional fields).
* Breaking changes require new major version (`/api/v2`).
* Clients must not rely on ordering of arrays.
* Deprecation notices announced one version ahead.

---

## **10. Acceptance Criteria (Definition of Done)**

Contract is considered met when:

✔ All endpoints respond exactly as defined above
✔ All schemas validated against this data contract
✔ Role-based access enforced as specified
✔ Error contract consistently applied
✔ SLOs validated via performance testing
✔ Documentation published for API consumers

---

## 📎 **Appendix A — Required Meetings for Contract Creation**

### **A.1 Requirements Discovery**

**Participants:** Product Owner, Architect, BA
**Output:** Inputs for SRS

### **A.2 Contract Definition Workshop**

**Participants:** Architect (Lead), PO, Lead Dev, Security
**Output:** Draft ACS

### **A.3 Feasibility Review**

**Participants:** Architect, Dev, QA, Security
**Output:** Approved ACS

### **A.4 Formal Sign-Off**

**Participants:** PO, Architect, Tech Lead, QA Lead
**Output:** Version-controlled ACS baseline

### **A.5 Change Control**

**Participants:** Architect, PO, Consumer reps
**Output:** New ACS version release


----

# 📄 **Document 3: Software Design Document (SDD / SAD)**

### **SPA-PAM – System Architecture & Design**

---

## **1. Introduction**

### **Purpose**

This Software Design Document describes **how** the SPA-PAM application will be implemented.
It translates the **SRS** and **ACS (2.5 Contract)** into an internal technical design for developers and architects.

### **Scope**

Covers frontend, backend, data storage, integration points, deployment, and internal flows.

### **References**

* Project Charter
* SRS
* ACS (Architecture Contract Specification)
* Test Plan
* Deployment Plan

---

## **2. System Overview**

### **High-Level Description**

SPA-PAM is a MERN-stack web application that enables breeders to post dog listings and customers to browse, save favorites, and message breeders. Admins oversee the system.

### **Architecture Style**

* **Frontend:** SPA (React + Vite)
* **Backend:** Layered Node.js / Express REST API
* **Storage:** MongoDB Atlas (document-oriented)
* **Images:** AWS S3 with signed URL retrieval
* **Hosting:** CloudFront + S3 + App Runner (or EC2)

### **Technology Stack**

* React 18
* Node.js 20
* Express.js
* MongoDB Atlas
* AWS S3 (image storage)
* CloudFront (frontend hosting)
* JSON Web Tokens (authentication)

---

## **3. System Architecture**

## **3.1 Architecture Diagram (Conceptual)**

*(Text-only representation; diagram can be added later)*

```
[React Frontend] 
      |
      v 
[Express API Layer] 
      |
      ├── User Service
      ├── Dog Service
      ├── Favorites Service
      └── Messaging Service
      |
      v
[MongoDB Atlas]

[Images] <--> [AWS S3 Signed URLs]
```

---

## **3.2 Component Descriptions**

### **Frontend (React/Vite)**

* Implements UI and all user-facing workflows.
* Stores JWT in memory (or secure storage).
* Sends authenticated requests to backend.

### **Backend (Express)**

* Routing layer
* Validation layer
* Business logic layer
* Data access layer
* Security middleware

All backend modules follow the ACS contract boundary.

### **MongoDB Atlas**

* Stores users, dogs, messages, favorites
* Uses collections: `users`, `dogs`, `messages`
* Supports indexing for common queries (e.g., breed filtering)

### **AWS S3 (Image Upload + Retrieval)**

* Private bucket for breeder uploads
* GET Object signed URLs generated per request
* No public bucket access

---

## **4. Detailed Design**

---

## **4.1 Backend Modules & Components**

### **4.1.1 Auth Module**

**Responsibilities:**

* Registration/login
* JWT creation and verification
* Role validation middleware

**Interfaces:**

* Input: User credentials
* Output: Signed JWT

---

### **4.1.2 Dog Module**

**Responsibilities:**

* CRUD operations for dogs
* S3 image upload integration
* Public dog listing retrieval (filters + pagination)

**Interfaces:**

* `POST /api/dogs`
* `GET /api/dogs`
* `GET /api/dogs/:id`

**Dependencies:**

* S3 client
* Dog data layer

---

### **4.1.3 Favorites Module**

**Responsibilities:**

* Add/remove favorites
* Retrieve user's favorites

**Interfaces:**

* `POST /api/user/favorites/:dogId`
* `DELETE /api/user/favorites/:dogId`
* `GET /api/user/favorites`

---

### **4.1.4 Messaging Module**

**Responsibilities:**

* Customer ↔ Breeder messaging
* Inbox/outbox operations

**Interfaces:**

* `POST /api/messages/send`
* `GET /api/messages/inbox`

---

## **4.2 Database Design**

### **Collections**

#### **Users**

```
{
  _id: ObjectId,
  userId: String,   // public
  role: String,
  email: String,
  passwordHash: String,
  profileName: String,
  favorites: [String] // dogId list
}
```

#### **Dogs**

```
{
  _id: ObjectId,
  dogId: String,
  name: String,
  breed: String,
  sex: String,
  ageMonths: Number,
  imageKey: String, // NOT exposed externally
  breederId: String,
  location: String,
  available: Boolean
}
```

#### **Messages**

```
{
  _id: ObjectId,
  messageId: String,
  senderId: String,
  recipientId: String,
  content: String,
  sentAt: Date
}
```

---

## **4.3 API Design (Internal View)**

*(This is NOT the external contract — this section covers internal routing & flow)*

Example:

### **Endpoint: Create Dog Listing**

**Route:** `POST /api/dogs`
**Steps (internal):**

1. Auth middleware verifies token
2. Role guard ensures breeder role
3. Input validated against CreateDogSchema
4. S3 upload performed
5. Dog record saved
6. Public Dog Schema returned

---

## **4.4 Internal Error Handling Flow**

* All errors normalized by error middleware
* Error codes mapped from internal error types
* Logs written to server logs (not sent externally)

---

## **4.5 Validation Layer**

* Uses JOI or custom validators
* All emails, passwords, dog fields validated
* Prevents malformed input before business logic

---

## **5. User Interface Design**

### **5.1 Core Screens**

* Home / Dog Search
* Dog Details
* Customer Dashboard
* Favorites
* Breeder Dashboard
* Dog Creation Form
* Messaging Inbox
* Admin Panel

### **5.2 UI Standards**

* Responsive grid
* Clean UX (minimal clicks)
* Button styles consistent
* Error messages in-line
* Accessible color contrast

---

## **6. Security & Compliance**

* JWT Authentication
* Role-Based Access Control (RBAC)
* HTTPS required
* Signed S3 URLs for all image retrieval
* No PII leakage (breeder phone hidden)
* No internal IDs exposed
* Helmet/CORS configuration
* Logs include userId but omit sensitive content

---

## **7. Performance & Scalability**

### **Front-end**

* Lazy loading images
* Client-side caching
* Pagination for dog browsing

### **Back-end**

* Indexes on breed, sex, location
* Batch queries for favorites
* Node clustering (optional future)

### **Cloud**

* CloudFront CDN for static assets
* S3 origin for images
* Horizontal scaling possible

---

## **8. Error Handling & Recovery**

* All errors flow through shared middleware
* Retry logic on S3 failures (internal only)
* 500 errors logged with timestamp + request metadata
* Graceful failure on network outages

---

## **9. Appendices**

* Glossary
* Extended architecture diagrams
* Data dictionary
* Future roadmap (Payments, Notifications, Multi-filter search)



---

# 📄 **Document 4: Test Plan**

## **1. Introduction**

### **Purpose**

This Test Plan defines **how SPA-PAM will be tested** to ensure it meets the functional, non-functional, and contract-level requirements defined in the:

* SRS
* Architecture Contract Specification (ACS)
* Software Design Document (SDD)

### **Scope**

Testing covers all publicly accessible workflows and all internal service interactions.
Does *not* include system internals not exposed to users (code refactoring, internal-only data fields).

### **References**

* SRS
* ACS
* SDD
* Deployment Plan
* User Stories / Requirements Backlog

---

## **2. Test Objectives**

SPA-PAM testing aims to:

1. **Verify functional requirements**:
   All FRs (FR-1 … FR-N) function as described in the SRS.

2. **Validate architectural boundaries**:
   API behavior, schema compliance, error handling, and security must match the ACS.

3. **Validate non-functional requirements** (performance, usability, reliability, security).

4. **Identify and document defects** using the defect log.

5. **Ensure readiness for production deployment**.

---

## **3. Test Items**

### **Major areas included in testing:**

| Feature / Module         | Description                          |
| ------------------------ | ------------------------------------ |
| **Authentication**       | Login, registration, JWT handling    |
| **Breeder Dog Listings** | Create, update, delete dog profiles  |
| **Dog Search**           | Filters, pagination, detail view     |
| **Favorites**            | Add/remove favorites, list favorites |
| **Messaging**            | Customer ↔ Breeder messaging         |
| **Admin Features**       | Moderation, oversight                |
| **Image Handling**       | S3 upload + signed URL retrieval     |
| **Role Permissions**     | Customer/Breeder/Admin boundaries    |

### **Out-of-Scope**

* AWS billing/console UI
* Developer-local internal scripts
* Unreleased future features (payments, push notifications)

---

## **4. Test Levels**

### **4.1 Unit Testing**

Performed by developers.

* Validate individual functions (e.g., validator logic, utilities).
* Use Jest or Mocha.

### **4.2 Integration Testing**

Test interactions between modules:

* Auth + role validation
* S3 upload + dog service
* Favorites service + user service
* Messaging flow

### **4.3 System Testing**

End-to-end validation:

* Customer searches → views → messages → favorites
* Breeder creates dog → customers view → message
* Admin moderation flows

### **4.4 User Acceptance Testing (UAT)**

Performed by stakeholders.
Validates the system meets business and ACS expectations.

---

## **5. Test Approach**

### **Methodology**

A hybrid methodology:

* **Automated testing**: Critical, repetitive flows
* **Manual testing**: UX, edge cases, exploratory

### **Tools**

* Cypress (UI/E2E)
* Jest (Unit tests)
* Postman (API validation)
* MongoDB Compass (data verification)

---

### **Entry Criteria**

* All development tasks for the test cycle completed
* Test environment deployed and stable
* API and schema contracts validated

### **Exit Criteria**

* ≥ 95% of test cases passed
* All Critical and High defects resolved
* ACS acceptance criteria met
* UAT sign-off completed

---

## **6. Test Environment**

### **Environment Components**

| Layer    | Environment                     |
| -------- | ------------------------------- |
| Frontend | CloudFront staging distribution |
| Backend  | AWS (App Runner or EC2) staging |
| Database | MongoDB Atlas M0 (staging)      |
| Storage  | S3 test bucket                  |
| Browsers | Chrome, Firefox, Safari         |
| Devices  | Desktop, iPhone, Android        |

### **Test Data**

* Seeded users (admin, breeder, customer)
* Sample dogs (5 breeds, various ages)
* Synthetic messages
* Non-sensitive data only

---

## **7. Test Deliverables**

* Test Plan (this document)
* Test Cases (spreadsheet or TestRail)
* Automated test scripts
* Defect Log
* Daily/Weekly Test Reports
* Final Test Summary Report

---

## **8. Roles & Responsibilities**

| Role              | Responsibilities                      |
| ----------------- | ------------------------------------- |
| **QA Lead**       | Owns Test Plan, prepares test reports |
| **Developers**    | Write unit tests, fix defects         |
| **QA Testers**    | Execute manual & automated tests      |
| **Product Owner** | Defines UAT criteria                  |
| **End Users**     | Perform UAT and provide acceptance    |

---

## **9. Risks & Mitigation**

| Risk                    | Mitigation                     |
| ----------------------- | ------------------------------ |
| Requirements unclear    | Weekly walkthroughs with PO    |
| Flaky test environment  | Use stable staging environment |
| S3 rate limits in dev   | Use throttled test uploads     |
| Authentication failures | Reset tokens/environment daily |

---

## **10. Schedule**

Testing aligns with the release schedule:

| Phase               | Dates            | Notes                       |
| ------------------- | ---------------- | --------------------------- |
| Unit Testing        | Sprint Weeks 1–2 | Continuous                  |
| Integration Testing | Week 3           | Prior to staging deployment |
| System Testing      | Week 4           | Full regression             |
| UAT                 | Week 5           | Stakeholder sign-off        |
| Release Readiness   | Week 6           | Final report                |



---

# 📄 **Document 5: Deployment / Release Plan**

## **1. Introduction**

### **Purpose**

This Deployment Plan defines **how SPA-PAM is deployed into the production environment**, including required steps, environments, roles, risk mitigation, rollback procedures, and communication flow.

### **Scope**

Covers deployment of:

* SPA-PAM frontend (React + Vite → S3 + CloudFront)
* SPA-PAM backend (Node.js/Express → App Runner or EC2)
* MongoDB Atlas (existing cluster)
* S3 image-storage bucket for dog images
  (Production only; development/local deployment is out of scope.)

### **References**

* SRS
* Architecture Contract Specification (ACS)
* Software Design Document (SDD)
* Test Plan
* AWS Architecture Diagrams

---

## **2. Deployment Overview**

### **Deployment Strategy**

SPA-PAM uses a **phased blue/green-style deployment**:

* Deploy new backend version to a *staging service*
* Validate health + smoke tests
* Promote to production
* Deploy frontend to S3
* Invalidate CloudFront cache to push new assets

This reduces downtime and risk.

### **Environment Flow**

```
Local Dev → Staging → UAT → Production
```

### **Target Audience**

* Breeders
* Customers
* Admins
* Internal support teams

---

## **3. Roles & Responsibilities**

| Role                   | Responsibilities                                |
| ---------------------- | ----------------------------------------------- |
| **Release Manager**    | Coordinates deployment window & approvals       |
| **DevOps Engineer**    | Executes deployment scripts, updates AWS config |
| **Backend Developer**  | Confirms API health, validates logs/errors      |
| **Frontend Developer** | Builds & publishes frontend bundle              |
| **QA Team**            | Runs smoke tests post-deployment                |
| **PM**                 | Communicates deployment status to stakeholders  |

---

## **4. Deployment Steps**

## **4.1 Pre-Deployment Checklist**

* ✔ All acceptance tests passed
* ✔ ACS boundary validation completed
* ✔ All migrations reviewed
* ✔ Backup of MongoDB taken
* ✔ S3 buckets accessible from IAM roles
* ✔ Secrets validated in Parameter Store
* ✔ Maintenance window communicated

---

## **4.2 Deployment Procedure**

### **Backend Deployment (EC2/App Runner)**

1. Pull latest version from GitHub main branch
2. Build backend (`npm install`, `npm run build`)
3. Package Docker image (if using App Runner)
4. Upload image to ECR
5. Deploy to staging service
6. Run health checks (`/health`, `/api/status`)
7. Promote staging → production
8. Validate production logs for errors

---

### **Frontend Deployment (S3 + CloudFront)**

1. Run `npm run build` (Vite build)
2. Upload `/dist` folder to S3 bucket
3. Set correct MIME types
4. Invalidate CloudFront cache
5. Confirm new UI loads in browser
6. Validate routing (index.html fallback)

---

### **Database (MongoDB Atlas)**

* No schema migrations unless planned
* Validate indexes
* Validate network access & IP whitelist (if applicable)
* Monitor performance metrics during deployment

---

## **4.3 Post-Deployment Verification**

### **Smoke Test Checklist**

* Login (all roles)
* View dog listings
* Create a new dog (breeder)
* Add/remove favorites
* Send a message
* Admin dashboard loads
* Signed S3 URLs load images correctly

### **Backend Verification**

* Check logs
* Check API metrics
* Ensure no 500 errors in first 30 minutes

### **Frontend Verification**

* Page loads without cache artifacts
* Main flows accessible
* No console errors

---

## **5. Rollback Plan**

### **Rollback Triggers**

* Major outage
* Incorrect builds
* API failure or schema mismatch
* Severe defects found in smoke tests

---

### **Rollback Steps**

#### **Backend Rollback**

1. Redeploy previous stable App Runner/EC2 version
2. Reapply previous environment variables
3. Monitor logs

#### **Frontend Rollback**

1. Restore previous S3 build
2. Re-invalidate CloudFront cache

#### **Database Rollback**

1. Restore last known-good backup
2. Validate data integrity
3. Notify team of rollback actions

---

## **6. Communication Plan**

### **Before Deployment**

* PM notifies stakeholders of planned deployment window
* Release Manager alerts all teams

### **During Deployment**

* Status updates on Slack/email every 20–30 minutes
* Immediate alert on any blocker

### **After Deployment**

* Confirmation message upon success
* Summary of changes
* Any known issues

---

## **7. Risks & Mitigation**

| Risk                          | Mitigation                                   |
| ----------------------------- | -------------------------------------------- |
| CloudFront caching old assets | Force invalidation, version UI bundle        |
| S3 permission errors          | Pre-deployment IAM validation                |
| API downtime                  | Blue/green staging validation                |
| Incorrect secrets             | Validate Parameter Store mappings beforehand |
| MongoDB rate limits (M0 tier) | Run non-essential jobs off-peak              |

---

## **8. Schedule**

### **Standard Deployment Timeline**

| Activity              | Estimated Duration |
| --------------------- | ------------------ |
| Pre-deployment checks | 1 hour             |
| Backend deploy        | 20 minutes         |
| Frontend deploy       | 10 minutes         |
| Verification          | 30 minutes         |
| Contingency time      | 1 hour             |

### **Cutover Plan**

* Traffic switches to new backend version when promoted from staging
* CloudFront cache invalidation completes within ~5–10 minutes
* Full rollout completed after smoke tests


---
Here is your final document in the sequence — **Document 6: Project Closure / Post-Implementation Report**, fully mocked for the **SPA-PAM** project and using the same structure and syntax as the rest of your documentation suite.

---

# 📄 **Document 6: Project Closure / Post-Implementation Report**

---
## **1. Project Overview**

* **Project Name:** SPA-PAM (Single-Page Application – Pet Adoption Marketplace)
* **Project Sponsor:** DHS Software Engineering Apprenticeship Program
* **Project Manager:** Larry Lopez
* **Start Date:** Feb 2025
* **End Date:** Oct 2025
* **Purpose:**
  The SPA-PAM project was initiated to provide a secure, scalable, role-based marketplace where breeders, customers, and admins can manage dog listings, contact each other, and coordinate pet adoption activities.

---

## **2. Objectives vs. Outcomes**

| Charter Objective                                         | Outcome           | Notes                                                 |
| --------------------------------------------------------- | ----------------- | ----------------------------------------------------- |
| Build a full MERN stack MVP with breeder & customer flows | **Met**           | Fully deployed to AWS (App Runner + S3/CloudFront).   |
| Implement secure authentication (JWT + RBAC)              | **Met**           | 3 roles: admin, breeder, customer.                    |
| Support image uploads for breeders                        | **Met**           | Images stored via S3 + signed URLs.                   |
| Build messaging/inbox system                              | **Met**           | Inbox available for customers & breeders.             |
| Deliver admin moderation tools                            | **Partially Met** | Moderation dashboard MVP shipped; analytics deferred. |
| Achieve <300ms average backend response                   | **Met**           | Logged performance validated.                         |
| Implement payment flow                                    | **Not Met**       | Square Payments deferred due to priority shift.       |

---

## **3. Deliverables Summary**

### **Delivered**

* SRS, ACS (2.5 Contract), SDD, Test Plan, Deployment Plan
* Fully functional SPA frontend
* Node.js/Express backend with complete role-based routes
* MongoDB Atlas data layer
* S3 dog-image upload + signed URL integration
* Admin dashboard features (basic moderation)
* Production deployment pipeline
* Automated smoke tests

### **Not Delivered**

* Analytics dashboard for admins
* Premium membership payment workflow
* Multi-language support

Reasons: Resource constraints + reprioritization mid-project.

---

## **4. Performance Against Baselines**

### **Scope**

* 90% of scope delivered
* Adjustments made after Sprint 4 (payment moved to a future release)

### **Schedule**

| Planned  | Actual   | Variance                                         |
| -------- | -------- | ------------------------------------------------ |
| 8 months | 9 months | +1 month (due to AWS deployment troubleshooting) |

### **Budget**

* **Planned:** $0 (free-tier + existing tools)
* **Actual:** ~$15/month (CloudFront + App Runner usage)
* Slight overage due to increased traffic during testing window.

### **Quality**

* Total test cases: 142
* Passed: 136
* Failed: 6 (non-critical UX items)
* No major production incidents

---

## **5. Lessons Learned**

### **What Went Well**

* AWS S3 + CloudFront worked reliably for SPA hosting
* App Runner simplified backend deployment
* Splitting ACS before design greatly improved architecture clarity
* Modular API design reduced merge conflicts
* Test automation (Cypress/Playwright) caught several regressions early

### **What Didn’t Go Well**

* Image upload workflow required multiple redesigns (CORS, signed URLs)
* MongoDB M0 limits (connections/throughput) slowed down integration testing
* S3 permissions caused multiple deployment delays
* Initial requirements were too broad; contract helped realign scope

### **Recommendations**

* Move to MongoDB M10 if user load increases
* Adopt Infrastructure-as-Code (Terraform or CDK) to avoid manual AWS drift
* Define ACS earlier for future projects
* Add performance monitoring (Datadog, CloudWatch dashboards) earlier

---

## **6. Risks & Issues**

### **Risks That Materialized**

| Risk                               | Impact | Mitigation                                     |
| ---------------------------------- | ------ | ---------------------------------------------- |
| CORS errors on S3 image routes     | Medium | Added signed URLs; tightened bucket policies   |
| Deployment pipeline drift          | High   | Switched to App Runner for predictable deploys |
| API authentication inconsistencies | Medium | Consolidated AuthContext + route normalization |

### **Open Issues**

* Admin analytics missing
* Payment feature unimplemented
* Occasional slow queries on breeder listings due to non-indexed fields

---

## **7. Stakeholder Feedback**

### **Sponsor Feedback**

* Satisfied with MVP delivery, especially security model
* Asked for payments + analytics in next release

### **User (Breeder & Customer) Feedback**

* UI intuitive and easy to navigate
* Image uploads slow on mobile
* Messaging feature highly valued

### **Team Feedback**

* Good collaboration cadence
* ACS made development flow more predictable
* Need better test environments

---

## **8. Transition to Operations**

### **Handover Summary**

* Runbooks delivered to Support & DevOps
* S3/CloudFront deployment instructions included
* App Runner pipeline documented
* Monitoring using CloudWatch & AWS logs
* Emergency escalation: DevOps → PM → Sponsor

### **Owning Team**

* **Operations:** AWS maintenance (App Runner, S3, CloudFront)
* **Support:** Tier 1 (general), Tier 2 (technical)
* **Development:** Enhancement team (future features)

---

## **9. Approval & Sign-Off**

| Name            | Role                       | Signature | Date   |
| --------------- | -------------------------- | --------- | ------ |
| Project Sponsor | DHS Apprenticeship Program | ________  | ______ |
| Project Manager | Larry Lopez                | ________  | ______ |
| Lead Architect  | (Your Name Here)           | ________  | ______ |
| QA Lead         |                            | ________  | ______ |

