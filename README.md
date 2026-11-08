# Codex Migration Kit

**Take your local Codex chats, sessions, and custom skills to your next computer.**

A small, inspectable [Agent Skill](skills/codex-migrate/SKILL.md) for assisted export and import between Windows and macOS. It helps Codex inspect a backup, map project folders, preserve existing destination history, and verify the result.

**Status: experimental.** This is an instruction-based skill, not a universal importer or background synchronization service. The workflow was informed by a completed Windows → macOS migration; other device combinations still need actual-device validation.

```text
Old computer                         New computer
Local Codex data → portable backup → inspect and map → merge → verify
```

## Start here

Install directly from GitHub for Codex:

```sh
npx --yes skills add nisargkavi/codex-migration-kit --skill codex-migrate --agent codex --global --yes
```

Requires Node.js 22.20 or later. This uses the [Skills CLI](https://github.com/vercel-labs/skills) to install the skill across your projects. If it does not appear in Codex, restart the app.

Alternatively, download this repository, open its folder as your workspace in Codex, and ask:

```text
Install the local skill at ./skills/codex-migrate in my user skills directory.
Preserve an existing skill with the same name if its content differs.
```

For a manual install, copy the entire `skills/codex-migrate` folder into a skill location discovered by your installation. Current documented user locations are `~/.agents/skills` on macOS and `%USERPROFILE%\.agents\skills` on Windows. Some desktop installations also use `.codex/skills`; use the location your app actually discovers and avoid installing duplicate copies. See the [official skill discovery documentation](https://learn.chatgpt.com/docs/build-skills).

The skill has no permanent CLI, server, account, package installation, or MCP dependency. Codex may create temporary local helpers for the particular archive and app version, and may need a trusted decompressor or isolated runtime repair. If the skill does not appear after installation, restart Codex.

## Use it

On the **old computer**:

```text
Use $codex-migrate to export my local Codex history and custom skills
to a portable ZIP. Exclude credentials and machine-specific runtimes.
```

On the **new computer**, inspect first:

```text
Use $codex-migrate to inspect /path/to/codex-backup.zip.
My copied projects are in /path/to/projects. Only do a dry-run.
Show the path mappings, conflicts, and compatibility findings.
```

Then request the merge:

```text
Use $codex-migrate to merge that backup into this installation.
Map the old frontend-v2 project to /path/to/projects/frontend.
Preserve my existing chats and sign-in.
```

An existing copied `.codex` folder can be used instead of a ZIP. The skill discovers actual roots and versions; it does not assume that a Windows drive maps to a particular Mac folder. Codex stores local state under `CODEX_HOME`, which normally defaults to `~/.codex`. [Configuration reference](https://learn.chatgpt.com/docs/config-file/config-advanced).

## What moves

| Data | Default behavior |
| --- | --- |
| Available local conversations and sessions | Inspect identities and merge compatible records. Include compressed rollouts. |
| Project roots and chat associations | Remap to the supplied destination projects. |
| Custom skills and their resources | Copy portable content, repair links, and report conflicts or required runtime repair. |
| Included attachments, images, plans and visualizations | Preserve available files within the requested scope. |
| Existing destination history and sign-in | Preserve. |
| Credentials, cookies, installation identity and native runtimes | Exclude from export and retain destination equivalents. |
| Source repositories, worktrees and files outside the backup | Transfer separately unless explicitly included. |

A copied `.codex` folder may not contain skills installed elsewhere or attachments originally stored in a temporary directory. The skill reports omissions rather than claiming to recover absent files.

## Why this needs more than copying a folder

The workflow accounts for SQLite WAL files, compressed sessions, renamed project directories, duplicate identities, history byte offsets, and native versus legacy project records. It stages a merge and a recovery journal instead of replacing the destination with the source directory.

The desktop app can overwrite externally edited sidebar state while running. An import may therefore finish with a prepared offline step: quit Codex normally, let the disclosed one-time helper apply the staged update, then reopen and verify. A pending restart is reported as pending, not as a completed migration.

## Supported directions and evidence

| Direction | Workflow coverage | Actual-device evidence |
| --- | --- | --- |
| Windows → macOS | Included | The precursor migration was completed; the reusable skill still requires broader release testing. |
| macOS → Windows | Included | Not yet verified end to end. |
| macOS → macOS | Included | Not yet verified end to end. |
| Windows → Windows | Included | Not yet verified end to end. |

Compatibility depends on actual Codex storage versions, not just the OS pair. Unknown schemas produce a compatibility report before mutation. See [compatibility and release checks](docs/compatibility.md) and [synthetic evaluation cases](evals/cases.json).

This project does not provide continuous sync, concurrent-edit conflict resolution, cloud-conversation transfers between accounts, or recovery of data absent from the backup.

## Privacy

The skill directs file operations to local storage. It does not upload a backup, create a server, or enable telemetry. **That is not a promise of fully offline execution:** Codex may use a remote model, and content the agent reads may enter its context according to your Codex configuration.

Credential files are excluded by default, but old chats and custom files can themselves contain secrets. Keep backups and journals private. Do not attach your real `.codex` folder, credentials, or transcripts to a public issue. See [security and data handling](SECURITY.md).

## Repository layout

```text
skills/codex-migrate/
  SKILL.md                    Agent instructions and operation routing
  agents/openai.yaml          Codex display metadata
  references/
    export-import.md          Archives, portable scope, and offline apply
    path-mapping.md           Filesystems, project identities, and runtimes
    data-integrity.md         SQLite, history cursors, verification, recovery
docs/
  compatibility.md            Evidence and release checklist
  product-direction.md        Skill versus website, positioning, repo metadata
evals/
  cases.json                  Synthetic behavioral scenarios
```

Read [CONTRIBUTING.md](CONTRIBUTING.md) before proposing changes. The repository contains instructions and synthetic scenarios; it does not contain real user backups or a tested cross-version migration engine.

## Inspiration and related projects

Packaging follows the [Agent Skills specification](https://github.com/agentskills/agentskills), with examples from [Anthropic Skills](https://github.com/anthropics/skills), [Vercel Agent Skills](https://github.com/vercel-labs/agent-skills), and [OpenAI Plugins](https://github.com/openai/plugins). OpenAI's older [skills repository](https://github.com/openai/skills) is currently marked deprecated and points to plugins.

Related tools already exist: [Codex ReHome](https://github.com/CalebYcj/codex-rehome), its [migration skill](https://github.com/CalebYcj/codex-rehome-skill), and [Codex Session Transfer](https://github.com/myyimu/codex-session-transfer). This project focuses on a small skill with explicit inspection, mapping, recovery, and compatibility evidence. It does not claim to be the first migration tool.

See [repository patterns and presentation choices](docs/repository-inspiration.md) for what was borrowed from each reference.

## License

[MIT](LICENSE). Independent community project; not affiliated with or endorsed by OpenAI.
