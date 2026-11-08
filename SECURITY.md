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

## Changes addressing W011 in 0.1.1

[Snyk's issue reference](https://github.com/snyk/agent-scan/blob/main/docs/issue-codes.md#W011) classifies W011 as exposure to untrusted third-party content. Its [current risk guidance](https://github.com/snyk/agent-scan/blob/main/docs/risks.md#third_party_content_exposure) calls for isolation and limiting sensitive/destructive capabilities. This differs from a finding of malicious skill instructions, but remains relevant because backups can contain adversarial content.

Version 0.1.1 strengthens the workflow at that boundary:

- Local readers preserve opaque transcript bytes and expose only bounded metadata needed for migration decisions. Stored prompts, messages, code and source-defined descriptions are excluded from ordinary model-visible inventory.
- Extracted trees are kept outside the active workspace; archived AGENTS.md, configuration and skills cannot become ambient policy during inspection.
- Plan application is separate from inspection. Source values cannot grant permissions, select network destinations or add executable commands. Readers should run without credentials, outbound network or destination-write access where the host can enforce those controls.
- Imported custom skills are preserved in non-discoverable staging until restricted review or an independently trusted content match. Copying, activation and runtime repair have distinct status; pending review does not block chat migration.
- SQLite inspection uses staged copies, fixed queries and disabled extension loading; source schema text and SQL dumps are never executed as migration instructions.
- App verification emits bounded status/count summaries instead of exposing old message bodies to a migration-capable agent.

These are agent workflow requirements, not a bundled enforced parser/sandbox. A host that cannot provide the required restrictions must report the limitation and defer unsafe review or activation. No scanner suppression or risk-ignore setting is added. W011 can remain because preserving user-controlled data is still part of the skill's purpose; a changed instruction file does not prove that the directory's cached scan has been rerun or that residual injection risk is eliminated.
