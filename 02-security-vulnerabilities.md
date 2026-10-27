# Security Vulnerabilities Common in Vibe-Coded Apps

AI tools (Lovable, Cursor, Bolt, Claude, v0, Replit, etc.) repeatedly produce the same high-impact failures. These are not theoretical — multiple independent 2025–2026 scans of thousands of public vibe-coded apps keep finding the exact same patterns.

**These are critical.** Many of them allow full data dumps, account takeover, or secret theft with almost no skill.

## Top Critical Failures

### 1. Exposed Secrets in Client-Side Code (Critical)

- API keys, Supabase `service_role` keys, Stripe secret keys, database connection strings, OpenAI/Anthropic keys, JWT secrets hard-coded or left in the browser bundle.
- Frontend JavaScript is public. Anyone can open DevTools → Sources / Network and extract them.
- AI tools frequently generate this because “it just works” in the browser.

**Impact:** Attacker gets full privileged access to your backend, payment processor, AI budget, or database.

**Rule:** Never put any secret or privileged key in client-side code, environment variables that reach the browser, or public repos. Use server-side / edge functions only. Rotate anything that was ever exposed.

### 2. Missing or Broken Row Level Security (RLS) — especially Supabase (Critical)

- Tables left without RLS enabled, or with policies that only check “is the user logged in?” instead of ownership.
- The public `anon` key is designed to be in the browser. Without proper RLS it becomes a free database dump tool.
- Extremely common in Lovable / Bolt / Cursor generated apps.

**Impact:** Anyone can read or modify other users’ data, emails, payment status, or internal records.

See `08-supabase-rls-deep-dive.md` for concrete policies and tests.

### 3. Broken Object Level Authorization / IDOR (Critical)

- Endpoints check authentication but not ownership.
- Classic example: change `/api/user/123` or `/api/orders/456` to another ID and get someone else’s data.
- AI tools often generate “if (user) return data[id]” without verifying `data.user_id === user.id`.

**Impact:** Full read/write of other users’ resources.

**Rule:** Every data access path must enforce ownership or role checks server-side. Test with two different accounts.

### 4. Unprotected Admin Routes & Debug Endpoints (High–Critical)

- `/admin`, `/dashboard`, `/debug`, `/api/internal`, preview URLs, or management panels left open or only protected by obscurity.
- Sometimes protected only by a hard-coded password in the frontend.

**Impact:** Full application takeover or mass data access.

### 5. Cross-Site Scripting (XSS) (High)

- User input rendered without sanitisation (especially in AI-generated React/Vue templates or markdown renderers).
- Can lead to session theft, account takeover, or further key extraction.

**Rule:** Never trust user-controlled content. Use framework escaping, sanitisation libraries, and Content-Security-Policy.

### 6. Sensitive Files Left Public (High–Critical)

- `.env`, `.env.local`, source maps, `.git` directories, backup files, or internal config committed and pushed, or left reachable on the production server.
- Source maps often contain original source with secrets still visible.

**Rule:** Never commit secrets. Add proper `.gitignore`. Strip source maps from production builds if not needed. Block sensitive paths at the web server / CDN level.

### 7. Unverified Webhooks (High)

- Stripe, payment, or other webhook handlers that trust the payload without verifying the signature.
- Attackers can forge `payment_intent.succeeded` events.

**Rule:** Always verify webhook signatures with the provider’s secret before acting.

### 8. Hallucinated or Typosquat Dependencies (Medium–High)

- AI suggests package names that do not exist or are malicious lookalikes.

**Rule:** Verify every new dependency on the official registry before installing.

## Why AI Tools Keep Doing This

- They optimise for “make it work quickly” over “make it secure by default”.
- Secrets in the client remove the need for a backend during prototyping.
- RLS and ownership checks add complexity the model often skips unless explicitly instructed.
- Many templates and examples the models trained on are themselves insecure.

## Agent Rules (Non-Negotiable)

- Default to server-side for any privileged key or operation.
- When creating database tables (especially Supabase): enable RLS + ownership policies immediately.
- When generating any data-access or API route: include ownership/role checks.
- When generating admin or sensitive routes: require authentication + authorisation.
- Never leave debug, preview, or internal endpoints public in production.
- Refuse or heavily warn on any request that would deliberately put secrets in the client or disable RLS “just to make it work”.

## Quick Attacker Mindset Test

Assume the attacker has:
- Your public anon / publishable key
- The ability to call every endpoint directly
- Knowledge of common ID patterns
- Access to your client-side JavaScript

If they can still read or change other users’ data, extract secrets, or reach admin functions → the app is not ready.

These issues are critical. Fix them before launch, not after the first public report.
