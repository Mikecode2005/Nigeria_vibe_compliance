# Authentication, Authorisation & Secrets Hygiene

## Secrets (Critical)

- **Never** put secret keys, service-role keys, private API keys, database credentials, Stripe secret keys, or JWT secrets in:
  - Client-side JavaScript / React / frontend bundles
  - Public GitHub repos
  - Environment variables that are exposed to the browser
  - Source maps or error messages
- Assume anything that reaches the browser is public. Open DevTools → Sources and you will see it.
- AI tools frequently generate this pattern because putting the key in the client “just works” during prototyping.
- Use server-side / edge functions / backend-for-frontend patterns for any privileged operation.
- Rotate any key that was ever committed, shipped to clients, or left in a public repo.

## Authentication

- Use established providers or well-tested libraries (Supabase Auth, Clerk, Auth.js, etc.) rather than rolling your own crypto.
- Enforce strong password rules or passwordless / magic-link / OAuth where appropriate.
- Protect login, signup, password-reset, and MFA endpoints with rate limiting.
- Session tokens / JWTs should be httpOnly, secure, and have reasonable lifetimes + rotation.

## Authorisation — Broken Object Level Authorization / IDOR (Critical)

- Authentication (“who are you?”) is not the same as authorisation (“are you allowed to do this?”).
- Every API route or database policy that returns or modifies user data must check ownership or role.
- Classic AI-generated failure:
  ```js
  // BAD — only checks login, not ownership
  if (user) {
    return data[id];
  }
  ```
- Correct pattern: verify `data.user_id === user.id` (or equivalent role check) before returning or modifying.
- Test with two different user accounts. User A must never be able to read or change User B’s resources by changing an ID in the URL or request body.

## Unprotected Admin & Debug Routes (High–Critical)

- `/admin`, `/dashboard`, `/debug`, `/api/internal`, preview URLs, or management panels must require authentication + proper authorisation.
- Do not protect them only by obscurity or a hard-coded password in the frontend.
- Remove or lock down debug and preview endpoints before production.

## Common Vibe-Coding Failures

- Service-role key or Stripe secret in the frontend “so it just works”
- RLS disabled “temporarily”
- Admin routes protected only by not advertising the URL
- Password reset tokens that never expire or are guessable
- JWT secret hard-coded or left as the framework default
- Source maps left enabled in production, exposing original source and secrets

## Agent Rules

- Default to server-side handling of any privileged key.
- When generating data-access code, always include an ownership or role check.
- When generating auth flows, include rate limiting and basic abuse protection.
- When generating admin or sensitive routes, require authentication + authorisation.
- Refuse requests that would deliberately put secrets in the client or weaken access controls without a clear, documented, time-limited reason and a compensating control.
