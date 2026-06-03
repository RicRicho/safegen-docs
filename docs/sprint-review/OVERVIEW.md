# SafeGen — System Overview

## The Core Architecture

SafeGen builds a **parent-controlled registry of child phone numbers** and uses that registry to query social-media platforms for account registration evidence.

The inversion: instead of asking platforms to verify every user (expensive, slow, gameable), SafeGen asks platforms one question: "Is this number in the registry of known child numbers?"

---

## How Parent Verification Works

1. **Parent initiates**: enters the child's phone number on the SafeGen site.
2. **SafeGen sends a validation message** to that number.
3. **Parent confirms receipt** — proving physical access to the phone.
4. **Legal notice attached**: the confirmation constitutes the parent's legal statement that they are the parent or guardian of the account holder.
5. **Number is registered** in the parent-tagged child-number registry.

---

## How Platform Querying Works

Once the number is registered, SafeGen queries major social-media platforms to determine whether the number is associated with existing accounts.

Per-platform response:

| Signal | Indicator |
|---|---|
| Account present | Hazard triangle on platform icon |
| No account found | Thumbs-up |
| Unknown | Question-mark bubble |

---

## Return Checking

Parents can re-check any previously registered number using the child's phone at any time — no login required. The phone itself becomes the recurring verification token.

---

## The Registry as a National Standard

The parent-tagged registry creates a definitive data source:

- **Per-number**: is this number associated with a child?
- **Per-platform**: does this platform have accounts linked to child numbers?
- **Auditable**: regulators (e.g. Office of eSafety) can inspect the registry to verify platform compliance.

The proposed audit authority is the **Office of eSafety** (Australian regulator). Parent email addresses are stored one-way — retrievable only by the audit authority.

---

## Privacy Design

- No face scanning. No biometrics. No government ID required.
- Phone number is the verification anchor.
- Parent email stored one-way: retrievable only by the audit authority, not by SafeGen operators in plaintext.
- File contents of accounts are never accessed.
- The registry confirms *that* a number is child-associated; it does not reveal account content.

---

## Technical Architecture (Sketched)

- **HSM-backed mobile-number management** — secure registry for parent-verified numbers.
- **Parent-verified child-number registry** — the core data product.
- **Query API for social-media platforms** — how platforms check whether a number is in the registry.
- **Browser pattern** — page preloads with mobile number; validation message confirms parent access.
- **API pricing**: $0.01 per call; first 10,000 free.

---

## Patents

SafeGen's technology is covered by **three patents**, held by SafeGen as a company. IP is held inside AAV Trust.

---

## Commercial Context

- **Vendor entity**: R2 Labs Pty Ltd.
- **AATT (Age Assurance Technology Trial) materials** rate the platform at **TRL 7**.
- National licensing model: technology gifted at cost for Australian national use; SafeGen retains international licensing rights.
- Cost comparison: current age-verification methods cost $1.50–$3.20 per check. SafeGen targets $0.01 per API call.
