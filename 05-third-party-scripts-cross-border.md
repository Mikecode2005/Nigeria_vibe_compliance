# Third-Party Scripts & Cross-Border Data Transfers

Loading resources from servers outside Nigeria often transfers personal data (especially IP addresses) without the user ever noticing.

## Why This Matters under NDPA

- An IP address is personal data.
- When a browser requests `fonts.googleapis.com`, a Clarity/Hotjar script, a CDN, or most analytics, the visitor’s IP and other request metadata are sent to servers that may be outside Nigeria.
- That is a cross-border transfer under NDPA s.41–43.
- Transfers need adequacy, appropriate safeguards, explicit informed consent after risk disclosure, or another limited derogation. The basis must be recorded.

## Highest-Risk Common Patterns in Vibe-Coded Apps

1. **Google Fonts** loaded from `fonts.googleapis.com` / `fonts.gstatic.com`
2. **Microsoft Clarity / Hotjar / similar** session-replay or heatmapping scripts
3. **Google Analytics / Google Tag Manager / Meta Pixel** without consent gates
4. **Any CDN or third-party JS** that is not privacy-aware and is not consented to

## Recommended Defaults for Agents

- Prefer **self-hosted fonts** or privacy-friendly font solutions that do not phone home.
- Prefer self-hosted or privacy-respecting analytics where possible.
- If a third-party script is required:
  - Document the transfer basis.
  - Load it only after consent where the processing is not strictly necessary.
  - Prefer vendors that offer contractual safeguards or Nigerian/regional options.
- Never treat “everyone uses Google Fonts” as a legal defence.

## Agent Behaviour
When the generated code includes external stylesheets, scripts, or fonts from non-Nigerian domains:
1. Flag the cross-border issue.
2. Offer a self-hosted or privacy-friendly alternative.
3. If the external resource is kept, require a consent gate or documented safeguard where needed.
4. Avoid loading tracking or behavioural scripts before consent.

## Quick Self-Check
Open the Network tab on a clean visit. Any request leaving Nigeria that carries an IP or identifier before the user has consented is a potential problem.
