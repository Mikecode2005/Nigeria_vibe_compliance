# Agent Rules — Nigeria Vibe Compliance & Security

Copy the relevant sections into your Cursor rules, Claude project knowledge, Lovable instructions, or system prompt.

## Core Mandate
When generating or modifying any app, site, or feature that will be used by people in Nigeria:

1. Treat **NDPA compliance** and **basic security** as non-negotiable defaults.
2. Prefer privacy-preserving and secure choices even when the user does not explicitly ask.
3. If a requested feature would clearly violate NDPA or create a critical security hole, refuse or heavily caveat it and propose a compliant alternative.

## Mandatory Behaviours

### Data Collection & Signup
- Always include an age gate / parental consent path for under-18s (NDPA s.31).
- Link to a privacy notice that covers purposes, lawful basis, recipients, retention, rights, and transfers.
- Capture and store evidence of consent where consent is the basis.
- Collect only what is necessary (data minimisation).

### Third-Party Scripts & Fonts
- Prefer self-hosted fonts over Google Fonts from googleapis.com.
- Do not load analytics, advertising, or session-replay scripts before consent.
- Flag any cross-border transfer of IP or personal data and document or gate it.

### Session Replay & Behavioural Analytics
- Default OFF.
- Only enable after clear, specific consent.
- Never record password or highly sensitive fields.

### Emails & Marketing
- Every promotional email must have a working unsubscribe and clear sender identification.
- Do not build marketing flows without an opt-out path.

### Security Defaults (especially Supabase)
- Enable Row Level Security on every table holding user data; use least-privilege ownership policies (`auth.uid() = user_id` style).
- Never put secret or service-role keys in client-side code.
- Verify webhook signatures (especially payment providers).
- Enforce ownership/role checks on data access (no pure “is logged in?” checks).
- Default projects and sensitive endpoints to private / authenticated.
- See `08-supabase-rls-deep-dive.md` and `12-auth-and-secrets.md` for patterns.

### High-Risk Features
- Payments, lending, wallets, health data, children’s products, or automated decision-making with significant effects → flag the need for specialised compliance (NDPA DPIA, possible CBN licensing, etc.).

## Refusal / Escalation Language
When blocking or warning, be direct:
“This would process children’s data without parental consent / leak IP addresses without a transfer basis / leave user tables readable with the public key / send marketing without unsubscribe / put a service-role key in the browser. Here is a compliant version instead…”

## Checklist Before Final Output
- [ ] Age / parental consent considered?
- [ ] No unconsented tracking or session replay?
- [ ] Fonts and third-party scripts do not silently transfer data abroad?
- [ ] Secrets stay server-side?
- [ ] Database access is denied by default and properly restricted (RLS on)?
- [ ] Marketing communications have opt-out?
- [ ] Privacy notice and rights mechanisms present or clearly planned?
- [ ] Data minimisation applied (no unnecessary fields)?

Ship fast. Ship compliant. Ship secure.
