# Nigeria Vibe-Coded App Compliance & Security Guardrails

**For Nigerian founders, vibe-coders, and AI agents building with Lovable, Cursor, Claude, Bolt, v0, Replit, etc.**

This repo collects practical, agent-ready README files that prevent the most common **NDPA violations** and **security holes** that get vibe-coded apps into trouble with the NDPC (and security researchers).

Ship fast. Ship compliant. Ship secure.

## Full File List

| File | Focus |
|------|--------|
| [01-ndpa-data-protection.md](01-ndpa-data-protection.md) | Core NDPA 2023 + GAID 2025 (children, consent, cross-border, rights) |
| [02-security-vulnerabilities.md](02-security-vulnerabilities.md) | Top vibe-coding security failures overview |
| [03-cookies-tracking.md](03-cookies-tracking.md) | Cookie banners, analytics, session replay |
| [04-email-marketing.md](04-email-marketing.md) | Waitlist / launch emails, unsubscribe, consent |
| [05-third-party-scripts-cross-border.md](05-third-party-scripts-cross-border.md) | Google Fonts, CDNs, analytics leaking IP data |
| [06-cybersecurity-cybercrimes.md](06-cybersecurity-cybercrimes.md) | Cybercrimes Act basics + hygiene |
| [07-fintech-cbn-notes.md](07-fintech-cbn-notes.md) | High-level notes if you touch payments / financial data |
| [08-supabase-rls-deep-dive.md](08-supabase-rls-deep-dive.md) | **Detailed** Supabase Row Level Security patterns and anti-patterns |
| [09-sample-privacy-notice.md](09-sample-privacy-notice.md) | Skeleton privacy notice aligned with NDPA |
| [10-breach-incident-response.md](10-breach-incident-response.md) | What to do when personal data is exposed |
| [11-data-minimisation-retention.md](11-data-minimisation-retention.md) | Collect less, keep less, delete properly |
| [12-auth-and-secrets.md](12-auth-and-secrets.md) | Secrets hygiene, auth vs authorisation |
| [AGENT-RULES.md](AGENT-RULES.md) | Drop-in rules for Cursor / Claude / Lovable / any coding agent |
| [PRE-SHIP-CHECKLIST.md](PRE-SHIP-CHECKLIST.md) | One-page checklist before you launch |

## Why this exists

AI tools generate working apps extremely fast. They also generate the exact patterns that NDPC notices and security scans keep finding:

- Missing age gates → children’s data without parental consent
- Google Fonts / Clarity / Hotjar without consent → IP and behaviour data leaving Nigeria
- Supabase tables with RLS off or weak policies → anyone can read user data with the public key
- Secrets and service-role keys in client bundles
- Marketing emails with no unsubscribe
- Stripe webhooks without signature verification
- Broken object-level authorisation (IDOR)

These are not edge cases. Multiple independent scans of thousands of vibe-coded apps show the same failures repeatedly.

## How to use

1. Clone or copy the relevant `.md` files into your project.
2. Add `AGENT-RULES.md` (or the strictest parts of it) to your system prompt / Cursor rules / Claude project knowledge.
3. Run the pre-ship checklist before every public launch or significant feature.
4. Treat compliance and security as non-negotiable defaults, not afterthoughts.
5. For Supabase-backed apps, start with `08-supabase-rls-deep-dive.md`.

## Disclaimer

This is practical guidance for builders, not formal legal advice. Laws, NDPC guidance, and CBN circulars evolve. For regulated activities (especially payments, lending, health, education) get qualified advice. Penalties under NDPA can reach the greater of ₦10 million or 2% of annual gross revenue for controllers/processors of major importance (₦2 million / 2% for others), plus compensation orders and other sanctions.

---

Built for the Nigerian builder community. Contributions and corrections welcome.
