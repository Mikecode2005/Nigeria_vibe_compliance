# Fintech / Payments / CBN High-Level Notes

If your app touches payments, wallets, lending, or other financial services, additional regulators and rules apply on top of the NDPA.

## Key Points (not exhaustive)

- **CBN licensing & guidelines** apply to many payment and financial activities. Operating without the correct licence or ignoring circulars is high risk.
- **Data localisation**: CBN has directed that certain payment and financial transaction data generated in Nigeria must be stored and managed in Nigeria (phased timelines apply). Check current circulars.
- **KYC / AML / record-keeping**: Customer identification, transaction monitoring, suspicious activity reporting, and retention rules are mandatory for licensed entities.
- **NDPA still applies fully**: Being regulated by the CBN does not exempt you from data protection obligations. Children’s data, consent, cross-border transfers, and DPIAs remain relevant — often more so because financial data is sensitive.
- **Open banking, APP fraud rules, and new AML automation requirements** have been rolling out; timelines and obligations change. Stay current.

## Agent Guidance
- If the product involves moving money, holding balances, credit scoring, or acting as a payment intermediary, flag that specialised legal and licensing advice is required before launch.
- Do not treat a generic “payments integration” (Paystack, Flutterwave, etc.) as complete compliance. The underlying activity may still need licences or specific controls.
- Prefer architectures that keep regulated data in Nigeria where localisation rules apply.
- Document data flows carefully — regulators and the NDPC both care where data goes.

This file is a pointer, not a compliance programme. Fintech is heavily supervised; get qualified advice early.
