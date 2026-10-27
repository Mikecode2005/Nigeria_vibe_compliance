# Authentication, Authorisation & Secrets Hygiene

## Secrets

- **Never** put secret keys, service-role keys, private API keys, or database credentials in:
  - Client-side JavaScript / React / frontend bundles
  - Public GitHub repos
  - Environment variables that are exposed to the browser
  - Source maps or error messages
- Assume anything that reaches the browser is public.
- Use server-side / edge functions / backend-for-frontend patterns for privileged operations.
- Rotate any key that was ever committed or shipped to clients.

## Authentication

- Use established providers or well-tested libraries (Supabase Auth, Clerk, Auth.js, etc.) rather than rolling your own crypto.
- Enforce strong password rules or passwordless / magic-link / OAuth where appropriate.
- Protect login, signup, password-reset, and MFA endpoints with rate limiting.
- Session tokens / JWTs should be httpOnly, secure, and have reasonable lifetimes + rotation.

## Authorisation (the part AI tools often skip)

- Authentication (“who are you?”) is not the same as authorisation (“are you allowed to do this?”).
- Every API route or database policy that returns or modifies user data must check ownership or role.
- Classic failure: endpoint checks `if (user)` then returns `data[id]` without verifying `data.user_id === user.id`.
- Test with two different user accounts. User A must never be able to read or change User B’s resources by changing an ID in the request.

## Common Vibe-Coding Failures

- Service-role key in the frontend “so it just works”
- RLS disabled “temporarily”
- Admin routes protected only by obscurity
- Password reset tokens that never expire or are guessable
- JWT secret hard-coded or left as the framework default

## Agent Rules

- Default to server-side handling of any privileged key.
- When generating data-access code, always include an ownership or role check.
- When generating auth flows, include rate limiting and basic abuse protection.
- Refuse requests that would deliberately weaken these controls without a clear, documented, time-limited reason and a compensating control.
