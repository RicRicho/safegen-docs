# SafeGen

**A parent-driven service for checking whether a child's phone number is registered on major social-media platforms.**

SafeGen gives parents a simple, privacy-respecting way to find out where their child's phone number is already being used online — and to build auditable evidence that platforms have not removed underage accounts they were notified about.

---

## The Problem

Social media platforms are required to protect children, but they cannot reliably detect underage users at scale. Face-based age verification is impractical for daily use and easy to circumvent. Telco-based approaches cannot distinguish between family-plan secondary lines, business lines, and genuine child accounts.

Meanwhile, 3,873 mobile numbers are definitively used by children, with zero cross-checks against social media platforms.

SafeGen proposes a different approach: **don't try to verify everyone. Build the registry of known child numbers. Let platforms query it.**

---

## How It Works

1. **Parent verifies number ownership** — a validation message is sent to the phone; the parent confirms physical possession. Combined with a legal notice that the parent is the authorised enquirer.
2. **SafeGen checks major social platforms** — the service queries whether the number is registered on major social-media platforms.
3. **Per-platform status is returned**:
   - Account present → hazard alert.
   - No account found → confirmed clear.
   - Unknown → platform-dependent uncertainty.
4. **Parent registry** — parent-tagged child numbers form a registry that can be audited by regulators (proposed: Office of eSafety).
5. **Return check** — parents can re-check using the child's phone at any time, with no login required.

---

## Why It's Different

- **No face scanning** — SafeGen does not require biometrics, live photos, or identity documents.
- **No telco dependency** — v1 works without telecom integration.
- **Privacy-preserving** — parent email addresses stored with one-way retrieval; accessible only by the designated audit authority.
- **Cost-competitive** — current age-verification methods cost $1.50–$3.20 per check. SafeGen's model targets a fraction of that cost at scale.

---

## Patent

SafeGen's technology is covered by three patents, held by SafeGen as a company. IP is held inside AAV Trust.

---

## Commercial Model

- API pricing: **$0.01 per call**, first 10,000 free, no credit card required.
- Vendor entity: **R2 Labs Pty Ltd**.
- National licensing model available for government / platform operators.

---

## Regulatory Context

SafeGen is designed to complement Australia's eSafety Age-Restricted Material Codes (effective March 2026) and aligns with international momentum on platform accountability for under-age access.

---

## Current State

Post-pivot design. Original Camara telco approach evaluated and superseded by the parent-driven model. Architecture defined. Commercial and government engagement ongoing.

---

## Inventor

**Ric Richardson** — `ricricho@gmail.com`

---

> *"Stop trying to verify everyone. Just block the known minors. The database is the product."*
