# 08. Technology & Security

## Stack Overview
- **Infrastructure:** Multi-cloud (Azure & AWS) with Kubernetes orchestration, Terraform-managed IaC, SOC 2 Type II certified.
- **Data Storage:** Snowflake data warehouse, PostgreSQL for transactional workloads, S3 for encrypted object storage (AES-256 at rest).
- **Processing:** Apache Spark for large-scale LCA computations, Python microservices (FastAPI), event-driven architecture via Kafka.
- **AI/ML:** Gradient-boosted models and graph neural networks for supplier impact scoring; explainability via SHAP dashboards.
- **Frontend:** React + TypeScript with component library following WCAG 2.1 AA accessibility guidelines.

## Data Model
- **Entity Graph:**
  - Facilities, suppliers, materials, transport legs, emission factors.
  - Time-series measurement tables with versioned baselines and adjustments.
- **Carbon Twin Simulation:** Monte Carlo scenario generator with constraint solver for cost and emission targets.
- **Audit Ledger:** Immutable log stored on QLDB (AWS) capturing evidence, reviewer signatures, and regulatory references.

## Security & Compliance
- SOC 2 Type II attested (report issued April 2024).
- ISO 27001 certification in progress (stage 2 audit scheduled Nov 2024).
- Data encryption in transit via TLS 1.3; key management handled by AWS KMS with quarterly rotation.
- Role-based access control integrated with SSO (Okta, Azure AD) and SCIM provisioning.
- Continuous vulnerability scanning (Snyk) and penetration tests by NCC Group annually.

## Privacy & Data Governance
- Data Processing Addendum aligns with GDPR and CCPA requirements.
- Data residency options: EU (Frankfurt), US (Virginia).
- Retention policy configurable per customer; default 7 years for audit logs.
- Dedicated data governance council reviews model changes and customer impact monthly.

## Reliability
- SLA: 99.5% uptime; actual trailing 12 months 99.8%.
- Disaster recovery: Active-active multi-region with RPO < 5 minutes, RTO < 30 minutes.
- Observability: Prometheus, Grafana, and Datadog APM with anomaly alerts to on-call rotations.

## Roadmap Considerations
- Building automated supplier verification via trusted oracles and zero-knowledge proofs.
- Expanding library of emission factors to include emerging hydrogen production pathways.
- Enhancing Carbon Twin with reinforcement learning for adaptive optimization.
