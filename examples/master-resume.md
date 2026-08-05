# **DANIEL MANSOUR**
**Software Engineer | First Principles Problem Solver**

Greater Houston, TX | [linkedin.com/in/demansou](https://www.linkedin.com/in/demansou)

---

## **PROFESSIONAL EXPERIENCE**

### **DealerBuilt** — Houston, Texas (Remote)
**Senior Software Engineer** | September 2022 – Present

Engineer driving the modernization of legacy monolithic automotive dealership software into cloud-native microservices architecture — as sole or lead developer across multiple platform domains (inventory audit, legal forms, and authentication/identity), plus cross-cutting technical leadership in production reliability, AI-assisted engineering practice, and platform strategy. Leading transformation efforts over 3+ years, decomposing .NET Framework monoliths into containerized services on AWS EKS.

#### **Inventory Scan Platform** — Solo Developer, September 2022 – March 2026
*Greenfield replacement of Windows CE scanners and locally-hosted audit software with cloud-native platform*

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

**Ownership Handoff (March 2026):**
- Planned and executed a full ownership transition to an incoming engineer — built from-scratch local-dev onboarding documentation and environment/secrets setup scripts, closed out alerting coverage gaps across all three environments, and shipped a set of self-service diagnostic tools so the platform could be triaged without the original developer
- Continued contributing targeted cross-cutting fixes post-handoff (dependency/CVE patches, a mobile-reporting UI feature) rather than a hard cutoff, easing the transition

#### **Forms Platform Modernization** — Solo Developer
*Replaced tightly-coupled Omnis 7 forms feature with cloud-native PDF generation platform*

**Problem:** Legal forms for vehicle sales/trades/leases were stored on hundreds of individual dealer computers. The form building team spent most of their time on repetitive PDF → XFDF → field mapping tasks, tracking calculations in Excel spreadsheets. They were perpetually behind, and form updates required working holidays/weekends because deployments couldn't be scheduled.

**Solution:**
- Designed AST-based formula resolution engine replicating Omnis calculation behavior and syntax for the web—modeled and replicated each Omnis function the team used, supporting database lookups, conditional logic, and arithmetic for PDF field mapping with per-rooftop variations
- Architected centralized cloud platform replacing forms stored across hundreds of dealer machines with single source of truth
- Built scheduled deployment system eliminating need for manual holiday/weekend form updates
- Designed React 19 form management UI + .NET 8 API with multiple bounded contexts for separation of concerns
- Created webhook integration enabling legacy desktop application to trigger cloud-based form provisioning
- Implemented OpenTelemetry distributed tracing across decomposed services
- Initiated a Go microservice for document handling and API support, which grew into a broader backend service over its first year

**Formula Engine — Legacy Semantics Parity at Scale:**
- Implemented sequential, position-dependent evaluation semantics for a legacy scripting language's mutable "hash variable" construct (60 reassignable slots reused mid-form) inside the production formula engine — a silent-correctness defect that could stamp legally-binding contracts with incorrect values without anyone noticing
- Delivered the fix via 7 additive architectural layers plus exactly one carefully validated engine-wide behavioral change, preserving a years-old shared engine's correctness contract across a ~10,000-line diff (30 commits)
- Grew the formula engine's test suite to 5,182 tests (+75 net) and validated the one behavioral change against all 9,272 production manifest rows with zero regressions, unblocking the broader legacy-forms migration effort that depended on it

**Legacy Forms Migration Tooling:**
- Built a differential testing harness comparing platform-computed field values against a harvested legacy ground-truth corpus down to the cent, giving the team a repeatable, low-risk parity gate for validating the migration
- Designed a linter-gated ingestion and triage pipeline (detect → convert → verify) for bulk legacy-form onboarding, replacing a manual process measured at roughly 17 developer-days for a single 108-form dealer batch
- Built an operator-driven migration workbench letting non-engineers round-trip PDF/field-mapping corrections without developer involvement
- Diagnosed and fixed a two-root-cause defect causing legacy-imported forms to render completely blank in production (a field-name/database-key mismatch plus a genuine capability gap), restoring 23 of 35 affected fields and scoping the remainder as an explicit, options-based product decision

**Billing Automation:**
- Designed a central, denormalized billing table with fail-safe parallel writes off the existing webhook flow, replacing a fully-manual, per-vendor spreadsheet reconciliation process that previously required querying hundreds of individual per-tenant databases across more than a dozen form vendors on different billing cadences
- Diagnosed and fixed a silent EF Core migration regression (a migration that looked valid but was a structural no-op against the real database) and a DateTime-normalization bug capable of silently shifting billing period boundaries by 6 hours on non-UTC servers; extracted a shared, regression-tested date-normalization utility to prevent recurrence

**Print & Document Bridge Architecture:**
- Designed a 6-state authentication state machine letting desktop users silently single-sign-on into an embedded web client window via cross-process messaging instead of re-authenticating, and built a standalone browser-based simulator to validate the flow without depending on the legacy desktop application or a working counterpart implementation — unblocking a circular dependency between two teams
- Reviewed and rewrote another team's implementation of the corresponding legacy-side auth bridge (a proprietary, non-diffable 4GL platform) via remote review, catching 3 critical missing pieces before it shipped and producing a self-serve handoff document in the other developer's native idioms
- Migrated PDF upload from an API-proxied pattern to presigned direct-to-storage uploads after root-causing intermittent false-positive rejections from a network firewall's content scanner; used a live-usage audit to tighten the signing principal's storage access from bucket-wide down to a small, verified set of prefixes
- Built a self-contained spike tool to empirically determine print-alignment tolerances on physical hardware, designing the production feature to be technique-agnostic so the answer could be swapped in behind a single interface with zero production code changes

**Service Consolidation Proposal (proposed, not yet executed):**
- After the Go service's original developer departed, authored a technical proposal to fold the Go microservice back into the team's primary .NET stack — citing duplicated deployment/pipeline/scaling overhead for a modestly-sized service and a raw-SQL bug class (NULL-vs-empty-string handling) that structurally cannot occur in the mature EF Core codebase; estimated at roughly one week of porting effort. Under consideration, not yet executed.

**Next-Generation Platform Migration Strategy:**
- Authored and own a multi-story epic defining how the forms, documents, and print domains migrate from the legacy platform onto the company's next-generation, greenfield DMS web platform
- Introduced an agentic planning framework to scope the migration at the initiative level, producing a detailed brownfield analysis grounded in real code references plus a dozen deepened architecture/requirements documents, one per migration story
- Authored and presented a platform architecture proposal reframing a narrow legacy-service-replacement effort into a single, extensible rendering platform covering every printable/signable document family company-wide; incorporated review feedback from principal architects and cross-functional leads and secured sign-off to proceed with phase 1

#### **Production Reliability Engineering & Root-Cause Analysis** — Cross-Platform

Beyond platform-specific ownership, maintains a systematic root-cause-analysis practice applied across every domain — GitOps/infrastructure, forms, inventory scan, and document-storage pipelines — consistently tracing production incidents to their true root cause rather than the first plausible explanation, and converting each into a durable fix plus a written RCA.

- Diagnosed a repeatedly-reverted production regression to a hidden circular dependency between application deployments and database migrations in the GitOps pipeline; while fixing it, audited the surrounding system and found four additional latent defects, including a months-long silent duplicate-job condition and a live configuration bug that would have deleted a cluster-critical service account on its next successful run — expanded automated validation coverage 5.5x in the process
- Traced a recurring cloud storage cost overrun (~$7,800/month) to an 18x gap between object count and application-level record count, caused by a timestamp-precision bug in a deduplication check; quantified over 97TB of reclaimable duplicate data across three independent verification methods and got the root-cause fix merged and confirmed live in production
- Root-caused a production image-registry retention policy that was silently deleting live production container images during routine cleanup, leaving every service in a latently broken state for over a week before a routine deployment surfaced it as a fleet-wide outage; redesigned the policy with separated production/development retention pools
- Diagnosed a ~24-hour multi-tenant production outage to an infrastructure cleanup step that had unknowingly broken a legacy API still silently serving several dealerships, and closed the detection gap from ~24 hours to under 30 minutes with new alerting
- Root-caused a fully-green, silently-failing mobile deployment pipeline to a redundant guard script that broke specifically on merge commits, closing the gap with a deploy-verification improvement
- Led a whole-codebase, multi-agent security and reliability audit spanning backend APIs, mobile, data integrity, and CI/CD, personally verifying every finding by direct code inspection before filing a prioritized backlog and packaging the highest-severity items into a cross-team, decision-driving handoff

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
- Consolidated GitOps from a three-branch-per-environment model down to a single-branch, path-based model across multiple EKS clusters, pairing each step with new CI validation (manifest schema + build checks) on every GitOps-managed path
- Migrated the last CloudFormation-managed frontends onto the same IaC/deployment pattern used elsewhere, eliminating roughly 90 cloud resources across 6 stacks in favor of about 18, and retiring a second IaC toolchain
- Built a reusable, zero-new-vendor-spend alerting pipeline (CloudWatch → SNS → Teams) covering two previously-unmonitored domains, and root-caused two separate silent-failure traps in the delivery chain (a KMS-encrypted topic silently dropping deliveries, and a webhook trigger failing to auto-confirm subscriptions)
- Authored infrastructure guardrails following a production incident: redesigned container image retention policy (separated production/development pools) and pinned managed-database engine versions across environments to prevent unplanned, unsupported upgrades

**CI/CD Pipeline Evolution:**
- Originally built CI/CD in AWS CodePipeline, later simplified to Bitbucket Pipelines for reduced complexity
- Designed multi-service parallel build pipeline: 4 backend APIs (.NET, Go) + 4 frontends built concurrently
- Implemented changeset-based conditional builds—PR pipelines only build services with changed files
- Built GitOps deployment flow: pipeline pushes to ECR → updates Kubernetes manifests → Flux CD reconciles to EKS
- Created multi-environment promotion workflow with automated dev/staging deployments and manual production gates
- Integrated Testcontainers for PostgreSQL integration tests in CI
- Extended CI to validate every GitOps-managed manifest (schema and build validation) on every change, closing a gap where most infrastructure paths had no automated pre-merge check

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

**Identity Platform Consolidation (2026):**
- Led the consolidation of over a dozen scattered, largely unmaintained (multi-year-old) identity, MFA, SSO, and federation services into a single, dedicated platform repository, preserving complete git history per source service specifically to retain institutional knowledge for code nobody remembered the reasoning behind
- Independently verified which of the consolidated services were actually live in production versus already dead by checking real cloud telemetry rather than assuming from code, and surfaced a prioritized set of critical security findings (credential-hygiene gaps and missing access controls) for remediation
- Designed and built the CI/CD pipeline and infrastructure-as-code for the new platform from scratch, going from zero to a fully working, merged deployment pipeline within a single day

#### **AI-Assisted Engineering Practice** — Cross-Cutting Initiative, 2026

Built and drives adoption of a company-wide practice for using AI coding agents safely and productively in a legacy-modernization context, treating spec-driven development and automated verification as the guardrails that let agentic development scale without silent regressions.

- Built a spec-to-test pipeline that generates structured, machine-executable test plans (with explicit manual-review steps as first-class citizens) and an AI-driven executor that runs them against real, deployed environments via API/CLI/browser automation — collapsing 30-60 minute manual release-validation runs into a few minutes, and cutting re-validation after a fix to a single command
- Ran the pipeline against 8 feature validations in its first week alone, surfacing 7 real bugs and 4 previously-unknown infrastructure issues along the way — including, on its very first real run, discovering and live-fixing two production infrastructure blockers (a silently-broken GitOps deployment key and a missing environment secret) mid-validation rather than simply reporting a failure
- Built three deterministic (non-AI) tools binding formal specifications 1:1 to automated, real-database acceptance tests via a stable identity scheme that survives refactors — piloted as a proof of concept, then adopted as a mandatory workflow convention across the team's spec-driven development process
- Designed and built a multi-stage orchestration pipeline (plan → implement → test) that runs an entire batch of related work items through spec-driven development as one unit on a shared branch with a single combined review, in both human-gated and unattended modes — generalized out of a project-specific tool into a reusable internal library adopted by other engineers
- Designed a context-handoff system so multi-phase agentic workflows retain decisions and status across sessions and branches without manually re-deriving prior work
- Authored a company-wide inventory scoring AI-development guardrails (implementation, review, and release stages) as in-place, proof-of-concept, or not-yet-built — explicit about which safety mechanisms don't exist yet rather than overstating maturity

#### **Technical Leadership & Strategic Contributions**

- Authored and presented executive-facing decision memos evaluating multi-year platform strategy for a chronically-failing legacy system, explicitly rejecting a proposed fourth front-end rewrite by demonstrating through due diligence that the actual failing component had never been touched across three prior rewrite attempts; surfaced previously-undocumented security and compliance risks during the review and requested explicit executive decisions rather than presenting a fait accompli
- Authored a strategic proposal recommending engineer-built AI skills as the primary operator interface for a chronically bottlenecked manual authoring workflow, reframing a multi-day, engineering-capacity-constrained process as a natural-language skill invocation
- Presented a comprehensive architecture review of an entire platform's Kubernetes footprint (workloads, networking, CI/CD, security posture, observability, HA/DR) to the engineering team, explicitly flagging known architectural risks for team discussion rather than presenting a polished-but-incomplete picture

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

**Infrastructure:** OpenTofu, AWS (EKS, ECR, Cognito, Lambda, CloudWatch, SNS, S3, RDS, Amplify), Kubernetes, Flux CD, Azure

**Observability:** OpenTelemetry, Prometheus, Grafana, Loki, CloudWatch

**DevOps:** Docker, Kustomize, Testcontainers, Bitbucket Pipelines, Azure DevOps, Jenkins, Fastlane, OIDC Federation

**AI-Assisted Engineering:** Spec-driven development, AI agent orchestration & skill design, automated acceptance-test generation, Claude Code

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
