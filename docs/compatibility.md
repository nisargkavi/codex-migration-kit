# Compatibility and release checks

## Current evidence

The instructions were developed from a real Windows → macOS transfer of local conversations, plain and Zstandard-compressed sessions, custom skills, project roots, and presentation state. That migration required project renames, handling platform-dependent migration-file hashes, adjusting history offsets, and applying sidebar state after a normal app quit.

This is evidence for those observations, not proof that this reusable skill works unchanged with every version or with the other OS pairs. The new skill is an assisted workflow; it has no permanently bundled migration implementation.

| Scope | Evidence level |
| --- | --- |
| Windows → macOS precursor workflow | Observed on actual devices; not a complete regression suite for the new skill. |
| Synthetic inspection scenarios | Independent dry-run evaluations are recorded in [evaluation results](../evals/RESULTS.md). |
| macOS → Windows | Instructions included; actual-device validation required. |
| macOS → macOS | Instructions included; actual-device validation required. |
| Windows → Windows | Instructions included; actual-device validation required. |
| Unknown/new Codex storage schemas | Inspect first. No compatibility claim without a verified adapter. |

## Before claiming a direction is tested

Use disposable, synthetic accounts/data and record the source/target OS, app/CLI versions, schema versions, selected scope and observed result. Do not publish machine identifiers or private paths.

1. Export a consistent snapshot with both recent WAL activity and older compressed sessions.
2. Import into a destination containing its own chat and a project with a matching mapped root.
3. Exercise a renamed project, an absent project, a fork/subagent, an archived record, an identical duplicate and a divergent same-ID conflict.
4. Confirm destination credentials, built-ins, configuration, original chats and later-created chats survive.
5. Verify source preservation, archive bounds, database relationships, file references and valid history offsets.
6. Apply through a normal quit/reopen and check that imported chats and project roots are visible in the app.
7. Repeat import; verify identical inputs are a no-op.
8. Add a new chat after import, then test operation-scoped rollback without deleting that chat.
9. Record failures and unsupported behavior; do not upgrade the evidence label from a dry-run alone.

## Known boundaries

Local storage formats are implementation details and may change. A filename such as `state_5.sqlite` is not an API contract. Semantic compatibility matters in addition to matching columns or checksums.

A source archive can be incomplete, a copied WAL can be inconsistent, a cache can be stale, and a skill can depend on files outside `.codex`. Those cases need explicit reporting. A complete merge cannot be inferred from the number of files copied.

Browser-based and cloud-backed sessions are distinct from local Codex history. This skill does not transfer cloud account ownership, authentication, active terminal processes, live browser profiles, or unsaved application state.
