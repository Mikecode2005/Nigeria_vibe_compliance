# Data Breach & Incident Response Basics

A security incident that exposes personal data is both a cybersecurity event and a potential NDPA personal-data breach.

## NDPA Notification Duties (high level)

- Controllers must notify the **NDPC** of a personal data breach that is likely to result in a risk to the rights and freedoms of individuals — generally within **72 hours** of becoming aware (subject to the exact wording and guidance in force).
- Where the breach is likely to result in a **high risk**, affected individuals must also be notified without undue delay, in clear language.
- Keep records of breaches even when notification is not required.

## Practical First Steps When Something Goes Wrong

1. **Contain**
   - Revoke or rotate exposed keys/credentials immediately.
   - Disable public access to affected tables, endpoints, or storage.
   - Take vulnerable services offline if necessary.

2. **Assess**
   - What data was involved? (personal data? special category? financial? children’s?)
   - How many people?
   - Was it actually accessed or only exposed?
   - Is there ongoing risk?

3. **Preserve evidence**
   - Logs, access records, timestamps, configuration at the time of the incident.
   - Do not wipe systems until you have captured what you need.

4. **Decide on notifications**
   - NDPC (and any sector regulator if applicable).
   - Affected individuals if high risk.
   - Internal stakeholders and insurers if relevant.

5. **Remediate & document**
   - Fix the root cause (e.g. enable RLS, remove secret from client, close public endpoint).
   - Document timeline, decisions, and actions taken.
   - Review whether similar issues exist elsewhere in the system.

## Agent / Builder Prevention Focus

Most vibe-coded breaches that become public follow the same patterns:

- Missing RLS → data readable with anon key
- Secret keys in the browser → attacker uses them
- Public project / preview left open
- Webhook or admin endpoint without proper auth

Preventing these is far cheaper than responding after the fact.

## Minimum Preparedness

- Know who to contact internally and which external counsel/DPCO you would use.
- Have a simple list of systems that hold personal data.
- Know how to rotate keys and disable public access quickly.
- Keep the pre-ship security checklist as living practice, not a one-time exercise.

This is not a full incident response plan. For anything beyond a trivial exposure, get professional help quickly.
