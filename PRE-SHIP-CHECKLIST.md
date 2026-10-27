# Pre-Ship Checklist — Nigerian Vibe-Coded Apps

Run this before every public launch, major feature release, or when opening a previously private project.

## Data Protection (NDPA)

- [ ] Age gate + parental consent flow for under-18s (or clear justification why not needed)
- [ ] Privacy notice covers purposes, lawful bases, recipients, retention, rights, cross-border transfers
- [ ] Consent is specific, informed, affirmative, and withdrawable (no pre-ticked boxes)
- [ ] Marketing / waitlist emails have working unsubscribe + sender identification
- [ ] Session replay / advanced analytics default OFF and gated by consent
- [ ] Non-essential cookies / trackers blocked until consent
- [ ] Cross-border transfers (fonts, analytics, CDNs, SaaS) have documented basis or are avoided
- [ ] Data subject rights request path exists (access, erasure, objection, etc.)
- [ ] Only necessary data is collected (minimisation)
- [ ] Account deletion actually removes or anonymises personal data

## Security (Critical Items First)

- [ ] **No secrets** (service-role, Stripe secret, API keys, DB URLs, JWT secrets) in client-side code or public repos
- [ ] RLS (or equivalent) enabled and restrictive on every table with user/sensitive data
- [ ] Policies use ownership checks (`auth.uid() = user_id`), not just “is authenticated”
- [ ] Ownership / role checks on all data access endpoints (no pure IDOR)
- [ ] Admin, debug, and internal routes require authentication + authorisation
- [ ] Webhooks (especially payments) verify signatures
- [ ] No public `.env`, `.git`, source maps, or backup files reachable
- [ ] Preview / debug endpoints locked down or removed for production
- [ ] Rate limiting on costly or abuse-prone endpoints
- [ ] HTTPS enforced
- [ ] User input is escaped / sanitised (XSS protection)

## Product-Specific

- [ ] If payments / financial data: licensing and data-localisation obligations reviewed
- [ ] If children’s product or high-risk processing: DPIA considered
- [ ] Incident / breach notification contacts and basic process known

## Final Attacker Tests

- [ ] Tested as an unauthenticated attacker with the public/anon key
- [ ] Tested that User A cannot read or modify User B’s data by changing IDs
- [ ] Opened DevTools → Sources and confirmed no secrets visible in the bundle
- [ ] Tested that marketing emails and tracking respect opt-out / consent
- [ ] Agent rules or compliance notes included in the project for future changes

When in doubt, default to more privacy and more restriction. It is easier to loosen later than to clean up a breach or an NDPC notice.
