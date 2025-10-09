# Appendix. Carbon Accounting Standards Reference

## Framework Alignment Matrix
| Requirement | Description | CarbonKilos Coverage |
| --- | --- | --- |
| GHG Protocol Corporate Standard | Accounting and reporting for Scopes 1-3 emissions. | Full support with activity data ingestion, emission factor mapping, and consolidation workflows. |
| ISO 14064-1 | Specification for quantification and reporting of GHG emissions. | Templates for organization-level inventories, variance analysis, and management review. |
| ISO 14067 | Product carbon footprint quantification. | Product lifecycle modeling and SKU-level emission factors within Carbon Twin. |
| EU CSRD | Mandatory sustainability reporting for large EU companies. | Pre-built disclosure templates, double materiality assessment toolkit, assurance readiness checklists. |
| EU CBAM | Carbon border adjustment mechanism for imports into EU. | Embedded tariff calculator using Carbon Twin outputs for covered goods. |
| SEC Proposed Climate Rule | Climate-related disclosures for US public companies. | Scenario analysis reporting, risk narrative builder, attestation support via Assurance Module. |
| TCFD | Climate-related financial disclosures. | Scenario planning workspace linking emission reductions to financial impacts. |
| SBTi | Science Based Targets initiative commitments. | Target tracking dashboards, automated progress alerts, pathway validation exports. |

## Emission Factor Sources
- **Primary:** ecoinvent v3.9, DEFRA 2024, EPA SmartWay.
- **Secondary:** Industry association databases (World Steel Association, IATA), supplier attestations.
- **Quality Control:** Confidence scoring (A-D) with automated re-validation every quarter.

## Verification Workflow
1. **Data Collection:** Pull raw activity data via integrations; apply QA rules for completeness.
2. **Factor Assignment:** Match to emission factors based on geography, technology, and supplier-specific data.
3. **Computation:** Run Monte Carlo simulations for uncertainty ranges; record baseline and optimized scenarios.
4. **Review:** Sustainability lead reviews flagged anomalies; auditors access immutable ledger with evidence attachments.
5. **Certification:** Generate assurance package referencing applicable standards and sign-off trail.

## Glossary
- **Carbon Intensity:** Emissions per functional unit (e.g., kg CO₂e per ton of steel).
- **Scope 3:** Indirect emissions occurring in the value chain (upstream and downstream).
- **Carbon Twin:** Digital representation of supply chain emissions enabling scenario planning and optimization.
- **Verified Carbon Unit (VCU):** Tradeable carbon credit issued after third-party verification of emission reductions or removals.
