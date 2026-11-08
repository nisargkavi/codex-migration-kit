# Contributing

Keep the installable skill focused on local Codex migration. Put substantial conditional guidance in its references and maintain working links from `SKILL.md`. Use the Agent Skills frontmatter format and keep display metadata consistent.

For a behavior change, describe the concrete case, affected direction and version assumptions. Add or update a synthetic scenario in `evals/cases.json`, run the relevant dry-run or isolated transfer, and record what was actually verified. Matching text or checking that a heading exists is not behavioral validation.

Changes involving SQLite, archive extraction, identity conflicts, file rewrites or rollback need evidence that source data and unrelated destination data survive. Never evaluate against a contributor's live `.codex` directory by default.

Do not commit real archives, transcripts, credentials, browser data, environment files or raw database dumps. Use invented paths, IDs and content. Redact issue reports, and follow [SECURITY.md](SECURITY.md) for sensitive findings.

The repository intentionally has no permanent migration CLI. Add executable helpers only when a demonstrated reliability requirement justifies them, with meaningful isolated tests and clear supported formats. Do not hard-code one contributor's storage layout as a universal schema.

Documentation must distinguish proposed support, synthetic evaluation, and actual-device validation. Avoid stable/production/offline/sync claims without the corresponding evidence.
