# Cybersecurity Basics & Cybercrimes Act Notes

The Cybercrimes (Prohibition, Prevention, etc.) Act 2015 (as amended 2024) creates offences and obligations relevant to anyone running digital services in Nigeria.

## Practical Obligations for Builders

- **Protect systems and data**: Unauthorised access, system interference, and data interference are criminalised. Basic security hygiene reduces both legal and practical risk.
- **Incident awareness**: Significant cyber incidents often have reporting expectations (sector CERT / national CERT pathways and, separately, NDPA breach notification rules). Know your reporting channels before you need them.
- **Access control & logging**: Maintain reasonable access controls, authentication, and logs. This helps both defence and any later investigation or reporting.
- **No tools for crime**: Do not create, distribute, or leave exposed tools, credentials, or configurations that facilitate unauthorised access or other offences.
- **Service provider duties**: If you provide certain computer-based services, additional duties around fraud, security codes, and cooperation with lawful investigations can apply.

## Minimum Technical Hygiene (Agent Defaults)

- Enforce authentication and authorisation on all non-public endpoints.
- Use HTTPS everywhere.
- Keep dependencies updated; avoid known-vulnerable packages.
- Never leave default or weak credentials.
- Store secrets properly (not in client code or public repos).
- Enable MFA for admin and sensitive accounts where available.
- Have a basic incident response outline: who to notify, how to contain, how to preserve evidence.

## Relationship with NDPA
A security failure that exposes personal data is both a cybersecurity incident and a potential NDPA personal-data breach. You may have dual notification clocks and duties. Coordinate them.

## Agent Behaviour
- Prefer secure defaults (HTTPS, auth required, least privilege, no secrets in client).
- When generating admin panels, payment flows, or user-data endpoints, include authentication, authorisation, and basic rate limiting.
- Do not generate code that intentionally weakens security “for convenience” without clear warnings.
