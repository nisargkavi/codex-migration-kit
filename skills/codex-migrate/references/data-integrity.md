# Data integrity and recovery

## Discover storage rather than hard-coding it

The names below were observed in one Windows → macOS migration, not a public storage API:

| Observed store | What required coordination |
| --- | --- |
| `state_5.sqlite` | Thread identities and metadata, project roots, assignments, relationships and presentation records. |
| `thread_history_1.sqlite` | Turns, items and rollout projection/cursor state. |
| `session_index.jsonl` | Session identity/title index. |
| `sessions/...jsonl` and `.jsonl.zst` | Physical rollout files, including inherited/forked metadata. |
| `.codex-global-state.json` | Legacy/native project maps and sidebar state cached by the desktop app. |
| `sqlite/codex.db` | Additional app-local catalog data; not assumed to be the canonical conversation store. |

Inspect `sqlite_master`, table/column types, defaults, constraints, foreign keys, indexes and schema versions in staged snapshots. Matching database filenames or migration counts is insufficient. Migration-file checksums can differ because of platform line endings; compare actual structural and semantic compatibility without replacing the target migration ledger. A required unknown column or changed semantics needs an adapter that is verified against fixtures.

Do not copy source authentication/account ownership fields into a different account indiscriminately. Preserve record ownership semantics where needed and surface incompatible account or host boundaries. Moving local files does not move cloud conversations or grant access to another person's account.

## Identity and duplicate handling

Use stable thread, turn, item and file identities. Compare a canonical representation or content hashes where appropriate. These outcomes are different:

- New identity: insert in dependency order.
- Same identity and equivalent content: skip without changing destination data.
- Same identity with known append-only continuation: merge only with verified ordering and relationship semantics.
- Same identity with divergent history or different meaning: preserve both inputs and report the conflict. Do not silently prefer source, overwrite target, invent IDs, or call an ignored insert a successful merge.

Preserve existing destination IDs and map source project references consistently. Include foreign keys, subagent/fork relationships, read/pin/archive state within scope and attachment identities. Do not confuse deleted/orphan physical rollouts with active user-visible chats or automatically resurrect them.

## Rollouts and cached history

Check compressed archives before calling a rollout missing. Stream decompression with expansion limits. A missing history-cache row does not necessarily mean the underlying chat is absent, and a complete-looking cache does not prove that every attachment or source file exists.

A database may reference `example.jsonl` while storage contains `example.jsonl.zst`. Establish the installed app's resolver behavior before changing that reference. Preserve a supported compressed representation, or stage a validated decompressed rollout and update the corresponding references and cursors together. Do not silently label it missing, change only the filename, or assume every app supports a compressed fallback.

If changing JSONL metadata, preserve unrelated lines byte-for-byte. Record old/new byte boundaries, line ordinal conventions and affected thread relationships, including shared physical rollouts. Updating a path can change serialized byte length, including escaping and UTF-8 differences.

Convert applicable turn-start, turn-end and projection cursor offsets under verified local semantics, or invoke a supported history rebuild that preserves data. Do not derive offsets from guessed ordinal rules; end offsets and compacted rollouts can use different conventions. Existing caches may already be stale relative to compacted files. Compare valid source boundaries with valid resulting boundaries and distinguish pre-existing problems from newly introduced inconsistencies.

Keep unsupported compressed formats or unknown cursor layouts intact and report the limitation. Never delete a history database merely to force rediscovery without proving that all authoritative content can be reconstructed.

## Running app and atomicity

An app can hold sidebar/global state in memory and overwrite an external file edit. Back up and stage first; apply after a normal quit, checking the destination has not changed since the snapshot. Use supported app APIs when they cover the operation and account for the user's authorization.

For an offline helper, record an operation ID, scope, exact stores to change, precondition hashes/versions, bounded lifetime, backup paths, journal location, apply phases and status. Recheck the current destination at apply time. Do not overwrite a stale staged database after the user created another chat. Do not relaunch, kill or permanently monitor the app without an explicit request.

A SQL transaction cannot atomically commit several independent databases plus session files and JSON state. Record every committed phase and how to recover it. Prefer staged, validated file replacements and narrowly scoped SQL transactions over wholesale replacement. On failure, leave a clear failed/pending marker and preserve enough data to resume or reverse safely.

## Verification

Use checks appropriate to the actual change:

- Original input is unchanged; exported/staged files match the recorded hashes.
- `PRAGMA integrity_check` or an appropriate quick check passes, and foreign-key relationships hold.
- Source identities are accounted for as imported, identical, conflicted, intentionally excluded or missing; destination identities remain present.
- Session/attachment references resolve, or known source omissions are reported. A backup's filenames alone are not evidence of complete history.
- Old valid history offsets remain valid after edits; new cursor changes match the actual encoding and compression behavior.
- Mapped project roots point to the supplied destination directories and deduplication did not merge unrelated projects.
- A representative old chat is readable in the app, the sidebar points to expected roots after reopening, and custom skill resources are discoverable.
- Repeat import of unchanged data is a no-op. A dry-run leaves destination files, WAL and configuration unchanged.

Prefer metadata summaries. Do not post private transcripts or tokens in verification logs, GitHub issues, screenshots, or examples.

If application versions or migration records are absent, an inventory and structural comparison can still be useful. Label that evidence as limited; do not infer full app compatibility or complete conversation content from metadata-only fixtures.

SQLite reference: [Online Backup API](https://sqlite.org/backup.html) and [Write-Ahead Logging](https://sqlite.org/wal.html). The coordinated Codex-store observations above come from the precursor migration and require local verification in another installation.

## Operation journal and rollback

Record inserted record identities, reused/conflicted IDs, updates with before-values and expected after-values, copied/rewritten files with before/after hashes, created directories, backups, mappings and verification results. Keep the journal local with restrictive permissions because it may include private paths or content needed for recovery.

Rollback should undo only this operation. Before reverting a row or file, confirm it still matches the recorded post-migration state. Preserve chats, replies, files and settings created or changed afterward; if changes overlap, report a recovery conflict and stage a targeted restoration.

A full pre-migration database backup is useful disaster recovery, but replacing the current database with it can erase later conversations. Do not perform that rollback automatically. If no sufficiently precise journal exists, explain the limitation and prepare the least destructive recovery supported by the available evidence.
