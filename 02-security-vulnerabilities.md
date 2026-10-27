# Security Vulnerabilities Common in Vibe-Coded Apps

AI tools (Lovable, Cursor, Bolt, Claude, v0, Replit, etc.) repeatedly produce the same high-impact failures. These are not theoretical — multiple 2025–2026 scans of thousands of public vibe-coded apps found the same patterns.

## Top Failure Patterns

### 1. Missing or Broken Row Level Security (RLS) — especially Supabase
- Tables in exposed schemas without RLS enabled, or with overly broad policies.
- Public anon key (intended for the client) can then read/write arbitrary rows.
- Result: anyone can dump user tables, change data, or escalate privileges.
- **Rule**: Enable RLS on every table that holds user or sensitive data. Write least-privilege policies. Test with the anon key as an unauthenticated attacker would.

### 2. Secrets in Client-Side Code
- OpenAI / Anthropic / Stripe / Supabase `service_role` / other API keys hard-coded or left in the browser bundle.
- Frontend code is public. Treat any key that reaches the browser as compromised.
- **Rule**: Never put secret or privileged keys in client code. Use server-side / edge functions / environment variables that stay on the server. Rotate anything that was ever exposed.

### 3. Broken Object-Level Authorization
- Endpoints that check “is the user logged in?” but not “does this user own this resource?”.
- Classic IDOR / BOLA.
- **Rule**: Every data access path must enforce ownership or role checks server-side.

### 4. Public-by-Default Projects & Previews
- Preview URLs, public projects, or open database endpoints indexed or guessable.
- **Rule**: Default to private. Explicitly decide what is public. Remove or protect debug/preview endpoints before launch.

### 5. Unverified Webhooks (especially Stripe)
- Webhook handlers that trust incoming events without verifying the signature.
- Attackers can forge `payment_intent.succeeded` etc.
- **Rule**: Always verify webhook signatures with the provider’s secret before acting on the event.

### 6. Hallucinated or Unvetted Dependencies
- AI suggests package names that do not exist or are typosquats.
- **Rule**: Verify every new dependency exists on the official registry and has a reasonable reputation before installing.

### 7. Missing Rate Limits & Auth on Sensitive Endpoints
- LLM proxy endpoints, password reset, signup, or expensive operations left open.
- **Rule**: Authenticate and rate-limit anything costly or sensitive.

### 8. Debug / Source Maps / .env / .git Exposed
- Source maps, `.env`, `.git`, backup files, or internal config left publicly reachable.
- **Rule**: Ensure production builds strip source maps if not needed, block sensitive paths, and never commit secrets.

## Agent Rules
- When scaffolding a database (especially Supabase): enable RLS and generate restrictive policies by default. Call this out explicitly.
- When adding any third-party API key: keep it server-side only. Refuse to put secrets in client components.
- When generating webhook handlers: include signature verification.
- When generating auth or data-access routes: include ownership/role checks.
- Prefer deny-by-default access patterns.
- Flag any public preview or open endpoint and recommend locking it down before production.

## Quick Test Mindset
Assume an attacker has:
- Your public anon / publishable key
- The ability to call your API endpoints directly
- Knowledge of common ID patterns

If they can still read or modify other users’ data, the app is not ready.
