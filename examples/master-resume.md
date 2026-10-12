# **DANIEL MANSOUR**
**Software Engineer | First Principles Problem Solver**

Greater Houston, TX | [linkedin.com/in/demansou](https://www.linkedin.com/in/demansou)

---

## **PROFESSIONAL EXPERIENCE**

### **DealerBuilt** — Houston, Texas (Remote)
**Senior Software Engineer** | September 2022 – Present

Engineer driving the modernization of legacy monolithic automotive dealership software into cloud-native microservices architecture. Led transformation efforts over 3+ years, decomposing .NET Framework monoliths into containerized services on AWS EKS. Sole developer of the identity/MFA platform and all of its infrastructure, sole owner of a document-archive platform inherited from its original developer, and primary engineer on the forms backend and admin UI; a core contributor on a team of roughly a dozen engineers rebuilding the dealership management system as a next-generation web platform.

#### **Inventory Scan Platform** — Lead Developer, 3+ years
*Greenfield replacement of Windows CE scanners and locally-hosted audit software with cloud-native platform. API, web, and auth surfaces led by me; the Android apps are shared with a second engineer.*

- Led redevelopment of Windows CE scan gun to modern RESTful API and Android application (unblocked revenue stream, 6% beta adoption rate)
- Designed inventory audit process allowing warehouse managers to audit during business hours rather than 24+ hour shutdowns (decreased warehouse down time by 100%)
- Developed variance calculation engine comparing scanned vs. expected inventory with cost and quantity tracking
- Built mismatch detection system flagging inventory integrity issues (same part in multiple bins)
- Implemented Zebra thermal printer integration via browser API with ZPL label generation
- Built React 19 frontend with TanStack ecosystem (Router, Query, Form) and MUI components

**Architecture Evolution:**
- Migrated from AWS Lambda to containerized .NET 8 API deployed on Kubernetes (EKS) with load balancing
- Optimized database performance to eliminate message queue dependency (removed SQS), enabling synchronous variance calculation
- Implemented OpenTelemetry distributed tracing and structured logging for improved observability

**Production Incident Response & Resiliency Upgrade:**
- Investigated production performance regression affecting large-scale warehouse audits (~2,500 parts, ~9,000 scans across 93 bins) — traced full hot path, identified O(n) linear scan on lazy IEnumerable as root bottleneck, fixed with HashSet materialization for O(1) lookups
- Conducted root cause analysis across the full observability pipeline; discovered the logging backend had been silently failing for weeks (storage exhaustion), rendering incident logs irrecoverable — documented findings and remediation in formal RCA
- Designed resilient async variance processing architecture using ASP.NET Core BackgroundService + Channel<T> pattern — eliminated infrastructure sprawl by replacing external queue dependency with in-process async processing and database state machine as distributed coordination primitive across horizontally scaled pods
- Built production-scale regression test suite using Testcontainers PostgreSQL, replicating real warehouse shapes (skewed bin distributions, rescans, mismatches) to catch performance degradation in CI
- Removed dead code paths and redundant allocations from the variance pipeline, reducing per-request memory overhead

**Multi-Tenant Database Architecture (Pioneered company-wide pattern):**
- First project at DealerBuilt to go full-in on cloud infrastructure, pioneering the routing pattern now used across the organization
- Architected dual-database system: central RDS database for application/audit state + hundreds of isolated tenant PostgreSQL databases containing dealership inventory
- Central database manages audit lifecycle (audits, bins, scans, variance calculations) while tenant databases serve as source of truth for real-time inventory data
- Pioneered use of existing PGBouncer infrastructure (previously only used by DBA team) for application-level tenant routing, enabling cloud-hosted APIs to dynamically connect to any tenant database based on JWT claims
- Implemented inventory writeback system syncing audit results from central database back to tenant-specific inventory tables, ensuring dealerships see up-to-date data in their ERP

#### **Forms Platform Modernization** — Primary Engineer (backend, admin UI, and infrastructure)
*Replaced tightly-coupled Omnis 7 forms feature with cloud-native PDF generation platform*

**Problem:** Legal forms for vehicle sales/trades/leases were stored on hundreds of individual dealer computers. The form building team spent most of their time on repetitive PDF → XFDF → field mapping tasks, tracking calculations in Excel spreadsheets. They were perpetually behind, and form updates required working holidays/weekends because deployments couldn't be scheduled.

**Solution:**
- Designed AST-based formula resolution engine replicating Omnis calculation behavior and syntax for the web—modeled and replicated each Omnis function the team used, supporting database lookups, conditional logic, and arithmetic for PDF field mapping with per-rooftop variations
- Architected centralized cloud platform replacing forms stored across hundreds of dealer machines with single source of truth
- Built scheduled deployment system eliminating need for manual holiday/weekend form updates
- Designed React 19 form management UI + .NET 8 API with multiple bounded contexts for separation of concerns
- Created webhook integration enabling legacy desktop application to trigger cloud-based form provisioning
- Implemented OpenTelemetry distributed tracing across decomposed services
- Own the Go document-handling service (DynamoDB/S3 storage), inherited from its original developer and still in active development as a deliberate interim platform: it keeps document handling reliable for current dealers, and it is scheduled for deprecation, not extension, once document handling moves onto the next-generation platform (see Document Archive & Migration Platform)

**2026 Delivery — Legacy Form Migration & Print:**
- Built the legacy-form migration path: importing forms from the legacy 4GL platform, correcting formula semantics on import, replacing legacy forms in place, auditing duplicate field keys with an operator runbook, and repairing imported field associations under controlled review
- Moved PDF intake to presigned direct-to-storage uploads
- Added print-job status polling, curbside no-deal form printing, and promote-by-deployment for PDFs; pinned frontend deploys to the exact version commit so releases are reproducible
- Built migration-reconciliation tooling: a source-owned change collector with advisory CI reports, used to verify the legacy and new platforms agree
- Wrote a Playwright flow-testing contract that is deliberately app-structure-agnostic: it layers e2e against unit and integration tests, derives specs from the OpenSpec requirements, and isolates app-specific behavior in fixtures, so the suite ports to the next-generation platform by swapping fixtures rather than rewriting specs
- Built a local multi-instance development environment with automated garbage-collection and stress tests so parallel worktrees and agents can run isolated stacks

#### **Infrastructure & Kubernetes** — Solo Developer (K8s with Technical Team Lead)
*First developer at company to migrate from Windows IIS to AWS cloud infrastructure*

**Evolution:** Initial AWS Lambda architecture led to iterative refinement:
- Started with individual Lambda functions per endpoint proxied through API Gateway, managed via CloudFormation
- Consolidated to single ASP.NET Core Lambda with internal routing to reduce deployment complexity
- Attempted Lambda warmers to mitigate cold starts, but only kept single instance alive—any scaling still triggered cold starts
- Ultimately migrated to Kubernetes (EKS) to eliminate cold start penalties entirely
- Transitioned IaC from CloudFormation to OpenTofu (Terraform) for K8s infrastructure management

**Current Architecture:**
- Collaborated with technical team lead to architect Flux CD GitOps platform on EKS
- Designed and implemented AWS infrastructure using OpenTofu (IaC)
- Built OIDC federation for CI/CD, eliminating long-lived AWS credentials in pipelines
- Orchestrated migration of services from Lambda to containerized deployments with zero downtime
- Established centralized observability with CloudWatch and OpenTelemetry

**CI/CD Pipeline Evolution:**
- Originally built CI/CD in AWS CodePipeline, later simplified to Bitbucket Pipelines for reduced complexity
- Designed multi-service parallel build pipeline: 4 backend APIs (.NET, Go) + 4 frontends built concurrently
- Implemented changeset-based conditional builds—PR pipelines only build services with changed files
- Built GitOps deployment flow: pipeline pushes to ECR → updates Kubernetes manifests → Flux CD reconciles to EKS
- Created multi-environment promotion workflow with automated dev/staging deployments and manual production gates
- Integrated Testcontainers for PostgreSQL integration tests in CI

**2026 CloudFormation Retirement & OpenTofu Adoption (identity platform, sole developer — all infrastructure is mine):**
- Retired 25 CloudFormation stacks (13 staging, 12 production) using a retain-then-delete procedure behind change-set gates, verified by clean OpenTofu plans afterward
- Adopted the existing 24 Lambda functions, API gateways, queues, CDN distributions, and IAM into OpenTofu with import blocks and no change to live configuration
- Replaced eight CodePipeline stacks with Bitbucket Pipelines using OIDC-assumed, repository-scoped roles under a permissions boundary; staging deploys automatically on merge, production sits behind a manual review gate
- Separated configuration from code deployment (infrastructure owns configuration, the pipeline owns function code) and added weighted-alias canary deploys with rollback targets for Lambda services
- Applied the same OIDC plan/apply pipeline pattern to the document-archive platform's staging and production environments

#### **Authentication Platform** — Solo Developer
*Replaced legacy desktop-only auth with multi-tenant AWS Cognito + OIDC*

**Legacy System:** Desktop-only authentication with no web support or MFA.

**Multi-Tenant Web Auth:**
- Pioneered multi-tenant web authentication using tenant database routing with dealer ID as third credential field
- Built foundation for web-based login across hundreds of tenant databases

**FTC MFA Compliance (2-week delivery):**
- Received emergency FTC mandate requiring MFA—delivered production-ready solution in 2 weeks
- Designed AWS Cognito migration strategy with Lambda triggers for one-time user migration on first successful login
- Built custom React AuthUI with Cognito SDK integration for user/password/dealer login flow
- Implemented MFA type selection (authenticator app or SMS) with custom UI flows
- Achieved FTC compliance despite rushed timeline; custom flow prioritized speed-to-market over strict OAuth2 conformance

**Internal Tools SSO:**
- Engineered true OIDC authentication for internal users via EntraID (Azure AD) → SAML → Cognito federation
- Enables secure access to internal web-facing tools without separate credentials

**2026 Identity Platform Consolidation (sole developer):**
- Consolidated ten separately maintained identity, MFA, SSO, and login services into a single monorepo with full history preserved and retired services archived; one pair of OpenTofu roots (staging, production) with seven shared modules
- Brought the managed Cognito user pools under OpenTofu management
- Enforced verified-location identity through a Cognito authorizer, rolled out in gated stages (staging first, then production) with refusal logging and repair of incomplete accounts
- Rebuilt the hosted authentication UI on React, Vite, and TanStack with per-environment custom domains, and added an SMS opt-in consent step to MFA enrollment

**2026 Least-Privilege & Security Remediation (identity platform, sole developer; scanner remediation also spans the document-archive and forms platforms):**
- Put permissions boundaries on service and authorizer roles, deleted a shared wildcard-scoped policy in favor of dedicated per-function policies, and narrowed CI plan-read access into scoped managed policies
- Added pipeline guards that verify IAM scope, scan diffs for secrets, and keep scanner exclusions documented with dated evidence
- Drove critical and high dependency and IAM scanner findings down across the identity, document-archive, and forms platforms (library upgrades, removal of vulnerable dependencies, committed lockfiles); open criticals reached zero on rescan and the remainder is tracked to owners

#### **Document Archive & Migration Platform** — Sole Owner (inherited), 2026
*Go and OpenTofu platform that migrates dealer documents into cloud storage on a nightly schedule and serves them to a web viewer. Taken over in production from its original developer, and kept deliberately interim: investment is scoped to reliability, safety, and a clean cutover, because the service is planned for deprecation when document handling moves to the next-generation platform.*

- Took sole ownership of a live production system inherited from its original developer, and made it dependable: the incidents and defects below were diagnosed, root-caused, and closed early in that ownership, and the operational knowledge now lives in runbooks and specs rather than in one person's head
- Merged three separate repositories (API, migration job, shared library) into one monorepo and moved container image builds out of `tofu apply` into the pipeline with immutable tags, removing the design that caused two production incidents in two days
- Diagnosed a fleet-wide nightly migration failure (image architecture mismatch) and hardened the build to verify the target architecture
- Root-caused a deduplication bug (timestamp-precision comparison) that re-uploaded unchanged documents indefinitely, leaving most stored bytes as duplicate object versions
- Built a read-only classification pipeline (S3 Inventory plus Athena) and then a content-aware cleanup job for the backlog: live re-derivation of every keep/delete decision, ETag-preconditioned deletes, runtime safety assertions, and dry-run on by default, because version deletes are irreversible
- Added continuous-backup health alerting to catch the silent failure mode where the change feed stops advancing and the recovery window quietly empties
- Migrated the document viewer frontend into the monorepo with a gated delivery path, moved it onto per-user authenticated access, and removed legacy key-compatibility code from the API authorizer
- Authored cutover, credential-rotation, and backup-health runbooks with as-run records

#### **Next-Generation DMS Web Platform** — Core Contributor (team of roughly a dozen engineers), 2026
*Ground-up rebuild of the legacy dealership management system as a multi-tenant web platform; forms is one module of it*

- Bootstrapped the spec baseline for the platform: 69 capability specs (OpenSpec) derived from the legacy sources and a prior platform
- Consolidated a prototype UI library into shadcn-based primitives in the web app, restructured it into feature and view layers, and set up Playwright e2e with CI plus a rule hierarchy for agent contributors
- Designed the forms-management domain aggregates and added architecture tests that check the DI graph and member-level boundaries
- Built the outbox-driven provisioning worker and generation orchestrator that carries forms from the management side to document generation
- Built the forms admin APIs: template upload and ETag-pinned promote/replace, a formula field catalog with server-side validation, and rooftop availability; added e2e specs for every template upload route
- Built a migration reconciliation register and validator, and authored the forms-migration PRD and architecture corpus and the planning trunk for the epics

**Print Platform — in flight** *(design and proof of concept delivered; build underway, not yet merged to the platform or piloted)*
- **Problem:** Dealership printing runs through a brittle chain of an embedded web view, the legacy desktop application, and a third-party PDF reader. It gives no reliable record of whether a job actually printed, and the new platform has no way to print without the legacy app. The work replaces that chain for forms office-PDF and dot-matrix (impact) printing with a platform-run print service and a native Windows client.
- **Architecture:** A cloud control plane inside the platform API, plus a signed, unattended Windows client per physical install: a supervisor service, an isolated print executor, native spooler submission (rasterized PDF through GDI, raw spooler writes for dot-matrix), an auto-updater with rollback, and an administrator setup app for enrollment. The client lives in its own solution with its own types and is tested against a contract mock, so it can be built and verified independently of the server.
- **Dispatch design:** I evaluated two dispatch shapes and chose "wake-up plus HTTPS claim". The real-time channel carries only a job-available nudge; job details and document links are released only through authorized, idempotent claims. The client reconciles on cold start, every reconnect, and a jittered safety poll, so a lost nudge costs latency but never a job. The design targets no lost jobs, no double prints, no cross-dealership routing, and no silent reprints, using a local attempt ledger and an explicit "ambiguous" outcome for the one case that cannot be known: a job that may already have reached the spooler.
- **Wire contract:** I authored a versioned print-service contract as the single source of the protocol, with one writer at a time and a changelog entry per change. It stays pre-1.0 until the claim and reconcile surface ships, then freezes with version negotiation. The server mints attempt identities, and each attempt carries a renewable lease; lease loss before spooling re-offers the job, and lease loss after spooling ends it as ambiguous.
- **Security model:** Each install enrolls once with a single-use, short-lived code and gets its own machine identity and a non-exportable key pair (TPM-backed where available). Tenant scope derives from server-side enrollment state rather than anything the client sends, and revocation closes the connection and suspends the install's printer mappings. Exceptions to the platform's tenant-scoping rules are recorded with owners and compensating controls.
- **Proof of concept:** A walking skeleton ran a real Windows service on a cloud VM against a dev cluster over a real WAN path, including the real machine-key authentication handshake. It was backed by a network-chaos test suite and a fleet simulator, and its findings drove the dispatch decision.
- **Where it stands:** The control-plane and client builds are substantially complete on epic branches, and the observability, support-bundle, runbook, and release-criteria work is drafted. Verification on real Windows hardware, the live code-signing pipeline, a physical dot-matrix print run, and a pilot cohort are still ahead. Nothing here is merged or in production yet.

#### **AI-Assisted Delivery Practices** — Across the above
- Deliver changes through a spec-driven (OpenSpec) process in all four codebases, with archived changes serving as the decision record
- Wrote a declarative local-validation contract: a table mapping changed paths to the validations required, mirroring the CI pipeline and including a tenant-data guard and a spec gate, so agents and engineers run the same checks before opening a PR
- Added agent-facing guidance to the repositories (rule hierarchies, a flow-testing guide) and repo-local agent skills for publishing and ticket authoring
- Run agent-driven delivery loops for batches of related changes, with automated code review in the PR workflow

---

### **Microsoft** — Remote
**Software Engineer** | June 2022 – September 2022

Short-term engagement on Microsoft Viva team, ended due to organizational restructuring.

- Built HR onboarding workflows for Microsoft Viva portal using React and SharePoint Framework (SPFx)
- Developed Adaptive Card Extensions (ACE) for mobile-first employee experiences
- Contributed to open source libraries supporting the Viva ecosystem
- Deployed services via Azure App Service, Logic Apps, CosmosDB, and Azure Functions

---

### **JPMorgan Chase & Co.** — Houston, Texas
**Software Engineer** | September 2020 – June 2022

Investment Banking technology team building enterprise productivity tools for 50,000+ employees globally.

- Built Microsoft Office 365 VSTO add-in combining brand compliance automation with productivity features—auto-applied corporate templates, inserted required disclaimers, and enforced document formatting standards
- Shipped two major add-in releases as enterprise installers deployed globally to 50k+ users
- Designed RESTful APIs with full-text search and NoSQL backends supporting the add-in's document management features
- Led infrastructure modernization: migrated backend services from Windows Server VMs to Kubernetes and CloudFoundry with Elasticsearch
- Owned agile process as team lead, collaborating with stakeholders and BAs to define MVP criteria and sprint priorities
- Maintained release stability through Jenkins CI/CD pipelines with automated testing and staged rollouts

---

### **HCSS** — Sugar Land, Texas
**Software Engineer (Contract)** | March 2020 – September 2020

Contract role building features for construction industry safety management software.

- Developed incident reporting and safety inspection features enabling field workers to document job site hazards in real-time
- Built digital inspection checklists replacing paper-based workflows for construction site compliance
- Implemented training and certification tracking to help contractors maintain OSHA compliance
- Managed Azure DevOps CI/CD pipelines and Azure cloud infrastructure supporting the SaaS platform

---

### **IPT Global, LLC** — Houston, Texas
**Software Engineer** | February 2018 – March 2020

Oil & Gas software for pressure test planning and leak detection—my first professional engineering role.

- Built pressure test planning interface enabling engineers to schedule and configure pipeline integrity tests
- Developed data visualization dashboards displaying real-time pressure readings and historical test results
- Implemented leak detection analysis features processing sensor data to identify pipeline anomalies
- Joined memory optimization team, profiling and reducing application memory footprint for field deployments on constrained hardware
- Led bi-weekly engineering education sessions, introducing team to new technologies and best practices
- Championed company-wide migration from legacy version control to Azure DevOps Git repositories

---

## **TECHNICAL SKILLS**

**Backend:** .NET 8, Go, C#, EF Core, AWS Lambda, PostgreSQL, DynamoDB, CosmosDB, Redis

**Frontend:** React 19, TypeScript, Vite, TanStack (Router, Query, Form, Table), TailwindCSS, MUI, WPF

**Infrastructure:** OpenTofu, AWS (EKS, ECR, Cognito, Lambda, API Gateway, CloudWatch, S3, Athena, RDS, SQS), Kubernetes, Flux CD, Azure

**DevOps:** Docker, Kustomize, Bitbucket Pipelines, Azure DevOps, Jenkins, OIDC Federation, OpenTelemetry, Canary Deploys

**Testing & AI-Assisted Delivery:** Playwright, Vitest, Testcontainers, OpenSpec (spec-driven development), Claude Code and agent workflows

**Architecture:** Monolith Decomposition, Microservices, Layered .NET, Monorepo, GitOps, Strangler Fig Pattern

---

## **EDUCATION**

### **Oregon State University** — College of Engineering
*School of Electrical Engineering and Computer Science (EECS)*
2015 – 2016 | GPA: 3.55

**Relevant Coursework:** Algorithms, Data Structures, Operating Systems, Software Engineering I & II, Databases, Web Development, Computer Networks, Discrete Mathematics

---

## **CERTIFICATIONS**

- **DEVOPS200.4x: Configuration Management for Containerized Delivery** — Microsoft (Sep 2019)
- **Machine Learning** — Coursera (Jul 2018)
