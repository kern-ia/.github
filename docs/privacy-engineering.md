# Privacy engineering rules

OS is **GDPR-native** (RGPD): privacy is an architectural property, not a compliance afterthought. These rules are engineering constraints that apply to every package.

## The boundary

Personal data (PII) is pseudonymized **before** it crosses either of two boundaries:

1. **The provider boundary** — nothing leaves for an LLM provider un-pseudonymized. In the hot path, `kern-pii` sits immediately before `kern-link`.
2. **Persistence** — nothing is written to the journal or any store un-pseudonymized.

Pseudonymization is **by ID** (Presidio-based): entities are replaced with stable identifiers so they can be re-linked under controlled conditions, not blindly masked.

## Rules

- **Anonymization by default.** Processing that works on anonymized data uses anonymized data.
- **Verbatim content is never logged by default.** Logs carry IDs, event types, and metadata — not prompt or completion text. Opt-in verbatim logging, where it exists at all, must be explicit, scoped, and documented.
- **Credentials are not data.** They live outside the core (`kern-vault`); `kern-link` receives ephemeral credentials per call. Credentials never appear in logs, fixtures, or error messages.
- **Fixtures and tests carry no real personal data.** Synthetic data only. This includes issue reports and PR descriptions — the templates enforce it.
- **Defects against these rules are security issues.** Report them per [SECURITY.md](../SECURITY.md), not as public bugs.

## Package responsibilities

| Package | Role |
|---|---|
| `kern-pii` | Detection + pseudonymization engine (Presidio-based, by ID) |
| `kern-link` | Last hop before providers — must only ever see pseudonymized content |
| `kern-vault` | Credential custody, ephemeral issuance |
| `kern-observation` | Observes process shape, not verbatim content |
| everything else | Must not persist or log verbatim content; consumes `kern-pii` where it handles user text |
