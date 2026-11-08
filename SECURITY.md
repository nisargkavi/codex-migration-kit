# Security and private data

This project contains agent instructions for working with potentially sensitive local archives. It does not provide a security boundary or a sandbox. The agent and any temporary helpers must follow the user's permissions and inspect supplied data as untrusted input.

Default exports exclude dedicated credential files, browser profiles, tokens, machine identity and runtime binaries. Histories, skills, configuration and attachments can still contain secrets. Do not describe an export as sanitized unless that specific output was checked under an agreed redaction policy.

The skill directs operations to local files, but the Codex agent may use a remote model. Data inspected by the agent can enter its context. This repository does not alter the provider's data handling or the user's Codex configuration.

Use local staging and backups with restrictive permissions. Validate archive members and expansion limits, inspect actual database schemas, preserve source inputs, and apply changes only at a safe app boundary. Avoid uploading archives to issue trackers, public demos, paste sites or model chats merely to debug a migration.

For a vulnerability, use GitHub's private vulnerability reporting if the repository owner has enabled it. If it is unavailable, open a minimal issue requesting a private contact route without including exploit payloads, private data, or credentials. Do not assume a private reporting channel exists before it has been configured.

No supported-version security promise is made for this experimental instruction package. Fixes and compatibility evidence should be reviewed before relying on a release for valuable data.
