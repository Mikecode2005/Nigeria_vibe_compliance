# Cookies, Analytics & Session Replay under NDPA / GAID

Non-essential cookies and tracking technologies require prior opt-in consent under the NDPA and GAID 2025.

## Key Rules

- **Strictly necessary** cookies (session, security, load balancing, accessibility) can be set without consent if they do not process sensitive data beyond what is needed.
- **Analytics, advertising, functional, and preference cookies** require clear, affirmative opt-in **before** they are set.
- Session-replay tools (Hotjar, Microsoft Clarity, FullStory, etc.) that record keystrokes, form inputs, mouse movements, or screens are high-risk. Default them **OFF**. Activate only after specific, informed consent. Never record password or sensitive fields.
- Consent must be freely given, specific, informed, and unambiguous. Pre-ticked boxes and “by continuing you agree” are invalid.
- Provide an easy way to withdraw consent and change preferences at any time.
- Cookie banner should appear in a prominent position (GAID discourages bottom-only placement that is easy to ignore).

## Practical Requirements for Agents

- Do not inject Google Analytics, Meta Pixel, Hotjar, Clarity, or similar scripts that fire on page load by default.
- Implement a consent gate: scripts only load after the user accepts the relevant category.
- Offer granular choices where practical (necessary / analytics / marketing).
- Link to a clear Cookie / Privacy Policy that explains each category, purpose, and retention.
- Session replay: explicitly require consent and document the high-risk nature.

## Common Failures
- Analytics and pixels loading before any consent interaction.
- Session replay left on by default “for debugging”.
- No reject / essential-only option.
- Banner that is hard to dismiss or that forces acceptance to use the site.

## Agent Behaviour
When adding any analytics, tracking, or session-replay tool:
1. Default to off / blocked.
2. Require a consent mechanism before the script runs.
3. Warn about cross-border implications (see third-party scripts file).
4. Prefer privacy-friendly, self-hosted, or Nigerian-friendly alternatives where they exist.
