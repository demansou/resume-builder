# **DANIEL MANSOUR**
**Senior Backend Engineer | Cloud Infrastructure & Platform**

Greater Houston, TX | [linkedin.com/in/demansou](https://www.linkedin.com/in/demansou)

---

*Tailored for: Senior Backend Engineer, Cloud Infrastructure role*

*Emphasis: Kubernetes, AWS, multi-tenant architecture, platform engineering*

---

## **PROFESSIONAL EXPERIENCE**

### **DealerBuilt** — Remote
**Senior Software Engineer** | September 2022 – Present

Solo developer leading cloud infrastructure modernization, migrating legacy .NET monoliths to containerized microservices on AWS EKS.

**Infrastructure & Platform:**
- Architected Flux CD GitOps platform on EKS with OpenTofu (Terraform) for infrastructure-as-code
- Built OIDC federation for CI/CD, eliminating long-lived AWS credentials
- Migrated services from Lambda to Kubernetes with zero downtime
- Designed multi-service parallel build pipeline: 8 services built concurrently with changeset-based conditional builds

**Multi-Tenant Architecture:**
- Pioneered company-wide multi-tenant database routing pattern using PGBouncer for dynamic tenant connection based on JWT claims
- Architected dual-database system: central RDS for application state + hundreds of isolated tenant PostgreSQL databases
- Built inventory writeback system syncing data between central and tenant databases

**Backend Services:**
- Migrated from AWS Lambda to containerized .NET 8 APIs on EKS
- Optimized database performance to eliminate SQS dependency, enabling synchronous processing
- Implemented OpenTelemetry distributed tracing and structured logging

---

### **JPMorgan Chase & Co.** — Houston, Texas
**Software Engineer** | September 2020 – June 2022

- Led infrastructure modernization: migrated backend services from Windows Server VMs to Kubernetes and CloudFoundry
- Designed RESTful APIs with full-text search and NoSQL backends
- Maintained release stability through Jenkins CI/CD pipelines with staged rollouts

---

## **TECHNICAL SKILLS**

**Infrastructure:** AWS (EKS, ECR, Lambda, RDS, S3, Cognito), Kubernetes, OpenTofu/Terraform, Flux CD

**Backend:** .NET 8, Go, PostgreSQL, DynamoDB, Redis

**DevOps:** Docker, GitOps, Bitbucket Pipelines, OIDC Federation, OpenTelemetry

---

## **EDUCATION**

**Oregon State University** — B.S. Computer Science (EECS), 2015–2016
