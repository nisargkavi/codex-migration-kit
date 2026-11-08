# Security and private data

This project contains agent instructions for working with potentially sensitive local archives. It does not provide a security boundary or a sandbox. The agent and any temporary helpers must follow the user's permissions and inspect supplied data as untrusted input.

Default exports exclude dedicated credential files, browser profiles, tokens, machine identity and runtime binaries. Histories, skills, configuration and attachments can still contain secrets. Do not describe an export as sanitized unless that specific output was checked under an agreed redaction policy.

The skill directs operations to local files, but the Codex agent may use a remote model. Data inspected by the agent can enter its context. This repository does not alter the provider's data handling or the user's Codex configuration.

The optional Vercel Skills CLI installer is a separate program with default installation telemetry and security-audit requests. Its documented opt-outs are `DISABLE_TELEMETRY=1` or `DO_NOT_TRACK=1` in the shell environment. See the README for the upstream documentation; the migration skill does not override these settings.

Use local staging and backups with restrictive permissions. Validate archive members and expansion limits, inspect actual database schemas, preserve source inputs, and apply changes only at a safe app boundary. Avoid uploading archives to issue trackers, public demos, paste sites or model chats merely to debug a migration.

For a vulnerability, use GitHub's private vulnerability reporting if the repository owner has enabled it. If it is unavailable, open a minimal issue requesting a private contact route without including exploit payloads, private data, or credentials. Do not assume a private reporting channel exists before it has been configured.

No supported-version security promise is made for this experimental instruction package. Fixes and compatibility evidence should be reviewed before relying on a release for valuable data.

## Directory audit observation

On 8 November 2026, skills.sh displayed a [Snyk W011 warning](https://skills.sh/nisargkavi/codex-migration-kit/codex-migrate/security/snyk): third-party content exposure and indirect prompt-injection risk from reading supplied archives, session history and custom skills. The report labels the issue MEDIUM and describes those sources as untrusted offline inputs. Reading such inputs is part of this migration workflow; the warning is not evidence that an archive has been made safe.

The skill instructs the agent to validate archive paths and expansion limits, treat archived instructions as data, avoid executing imported code, and preserve the source and destination. These measures reduce risk but do not turn a skill into a security sandbox. Agent Trust Hub and Socket were shown as passing separately; their results do not cancel the Snyk warning.
