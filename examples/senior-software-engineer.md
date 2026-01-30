# **DANIEL MANSOUR**
**Software Engineer | First Principles Problem Solver**

Greater Houston, TX | [linkedin.com/in/demansou](https://www.linkedin.com/in/demansou)

---

## **PROFESSIONAL EXPERIENCE**

### **DealerBuilt** — Houston, Texas (Remote)
**Senior Software Engineer** | September 2022 – Present

Solo developer driving the modernization of legacy monolithic automotive dealership software into cloud-native microservices architecture. Led transformation efforts over 3+ years, decomposing .NET Framework monoliths into containerized services on AWS EKS.

#### **Scan Platform (DSP/DSV)** — Solo Developer, 3+ years
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

**Multi-Tenant Database Architecture (Pioneered company-wide pattern):**
- First project at DealerBuilt to go full-in on cloud infrastructure, pioneering the routing pattern now used across the organization
- Architected dual-database system: central RDS database for application/audit state + hundreds of isolated tenant PostgreSQL databases containing dealership inventory
- Central database manages audit lifecycle (audits, bins, scans, variance calculations) while tenant databases serve as source of truth for real-time inventory data
- Pioneered use of existing PGBouncer infrastructure (previously only used by DBA team) for application-level tenant routing, enabling cloud-hosted APIs to dynamically connect to any tenant database based on JWT claims
- Implemented inventory writeback system syncing audit results from central database back to tenant-specific inventory tables, ensuring dealerships see up-to-date data in their ERP (Lightyear)

#### **Forms Platform Modernization** — Solo Developer
*Replaced tightly-coupled Omnis 7 forms feature with cloud-native PDF generation platform*

**Problem:** Legal forms for vehicle sales/trades/leases were stored on hundreds of individual dealer computers. The form building team spent most of their time on repetitive PDF → XFDF → field mapping tasks, tracking calculations in Excel spreadsheets. They were perpetually behind, and form updates required working holidays/weekends because deployments couldn't be scheduled.

**Solution:**
- Designed AST-based formula resolution engine replicating Omnis calculation behavior and syntax for the web—modeled and replicated each Omnis function the team used, supporting database lookups, conditional logic, and arithmetic for PDF field mapping with per-rooftop variations
- Architected centralized cloud platform replacing forms stored across hundreds of dealer machines with single source of truth
- Built scheduled deployment system eliminating need for manual holiday/weekend form updates
- Designed React 19 form management UI + .NET 8 API with 5 independent EF Core DbContexts (FormsMetadata, PdfDocument, XfdfDocument, Audit, Settings)
- Created Lightyear webhook integration enabling legacy Omnis desktop to trigger cloud-based form provisioning
- Implemented OpenTelemetry distributed tracing across decomposed services
- Initiated FTW (Forms To Web) Go rewrite for document handling with DynamoDB/S3 storage

#### **Infrastructure & Kubernetes** — Solo Developer (K8s with Technical Team Lead)
*First developer at company to migrate from Windows IIS to AWS cloud infrastructure*

**Evolution:** CEO mandate to use AWS Lambda for Scan microservices led to iterative architecture refinement:
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
- Built GitOps deployment flow: pipeline pushes to ECR → updates Scimitar manifests → Flux CD reconciles to EKS
- Created multi-environment promotion: develop→dev (auto), main→staging (auto-versioned), manual→prod
- Integrated Testcontainers for PostgreSQL integration tests in CI

#### **Authentication Platform** — Solo Developer
*Replaced legacy desktop-only auth with multi-tenant AWS Cognito + OIDC*

**Legacy System:** Desktop-only username/password checked against tenant database with password decryption—no web support, no MFA.

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

**Infrastructure:** OpenTofu, AWS (EKS, ECR, Cognito, Lambda, CloudWatch, S3, RDS), Kubernetes, Flux CD, Azure

**DevOps:** Docker, Kustomize, Bitbucket Pipelines, Azure DevOps, Jenkins, OIDC Federation, OpenTelemetry

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
