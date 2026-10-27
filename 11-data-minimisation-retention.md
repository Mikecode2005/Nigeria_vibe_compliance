# Data Minimisation & Retention

NDPA requires that personal data be:

- Adequate, relevant, and limited to what is necessary for the purposes (minimisation)
- Kept in a form that permits identification for no longer than necessary (storage limitation)

## Practical Rules for Agents & Builders

### Collect less
- Only ask for fields you actually need right now.
- Do not collect date of birth, phone, address, or ID documents “just in case”.
- Prefer anonymous or pseudonymous analytics where possible.
- Avoid free-text fields that invite people to paste sensitive information.

### Store less, for less time
- Define retention periods for each category of data.
- Automatically delete or anonymise data that is no longer needed.
- Separate marketing consent records from core account data so you can purge marketing lists cleanly.
- Logs and debug data should have short, enforced lifetimes.

### Design for deletion
- Every user-facing “delete my account” or “erase my data” flow should actually remove or irreversibly anonymise the personal data (subject to legal holds).
- Soft-delete flags are not enough if the data remains fully recoverable and identifiable indefinitely.
- Cascading deletes or anonymisation jobs for related tables (orders, messages, files, etc.).

### Special categories & children
- Heightened minimisation and retention discipline for health, biometric, financial, children’s, or other sensitive data.
- Prefer not to collect these categories unless the core purpose truly requires them.

## Agent Behaviour
When generating forms, schemas, or database models:

- Challenge unnecessary fields.
- Suggest retention columns or scheduled cleanup jobs where appropriate.
- Implement real account-deletion flows that remove personal data rather than only deactivating the login.
- Document the purpose of each data field so future changes can reassess necessity.

## Quick Test
For every field in your database or form, ask:
“If I remove this, can the core product still function?”  
If yes, strongly consider not collecting it.
