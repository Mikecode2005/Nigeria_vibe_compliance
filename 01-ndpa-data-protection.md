# NDPA Data Protection Guardrails
## Nigeria Data Protection Act 2023 + GAID 2025

You are generating or modifying code that will process personal data of people in Nigeria.  
Treat NDPA compliance as a first-class requirement — same level as security.

### Absolute Requirements

#### 1. Children’s Data (NDPA s.31)
- A child is anyone under 18 (Child’s Rights Act definition).
- Never collect or process a child’s personal data without verified parental/guardian consent (except narrow vital interest, education/medical/social care by professionals, or court proceedings).
- Implement an age gate + parental consent mechanism on every signup / data collection point.
- Prefer government-approved ID or strong age-assurance methods.
- If the product is likely to attract under-18s, design the entire flow around parental consent from day one.

#### 2. Cross-Border Transfers (NDPA s.41–43)
- IP addresses, device fingerprints, analytics IDs, and any personal data leaving Nigeria require:
  - Adequacy / approved safeguards (SCCs, BCRs, codes, certification), **or**
  - Explicit informed consent after risk disclosure, **or**
  - Another s.43 derogation.
- Record the basis for every transfer.
- Google Fonts from `fonts.googleapis.com`, many analytics, CDNs, and SaaS tools trigger this.

#### 3. Consent & Lawful Basis
- Consent must be freely given, specific, informed, unambiguous, and withdrawable.
- Silence, pre-ticked boxes, or “by continuing you agree” is **not** valid consent.
- Document the lawful basis for every processing purpose.
- Provide a clear privacy notice covering purposes, recipients, retention, rights, and transfers.

#### 4. Data Subject Rights
- Easy mechanisms for access, rectification, erasure, restriction, objection, portability.
- Honour opt-outs from direct marketing immediately and permanently.
- Respond within statutory timelines.

#### 5. Privacy by Design Defaults
- Minimise data collected.
- Prefer Nigerian-hosted or privacy-preserving alternatives where practical.
- Do not enable tracking, session replay, or non-essential cookies until consent is obtained.
- High-risk processing (profiling, automated decisions with significant effects, systematic monitoring, children’s data, cross-border) often requires a DPIA.

### Agent Behaviour
- Signup / waitlist / any data collection UI → include age verification + parental consent path + privacy notice link.
- Any third-party script → flag cross-border and consent implications; propose compliant alternative or consent gate.
- Never hard-code non-essential tracking or session replay to “on”.
- If a requested feature would clearly violate the above, refuse or heavily caveat and offer a compliant version.

### Penalties (reminder)
- Controllers/processors of major importance: greater of ₦10,000,000 or 2% of preceding year’s gross revenue.
- Others: greater of ₦2,000,000 or 2%.
- Plus compensation, remedial orders, possible criminal exposure for ignoring NDPC directives.
