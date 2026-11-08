# Product direction and GitHub positioning

## Recommendation

Release an inspectable migration skill first. A person usually needs device migration occasionally, but needs it to be reliable when it happens. A useful GitHub repository can serve that need without a frequently visited website or a service account.

The important scope is one-time local export/import. Continuous synchronization is a different product: it needs concurrency control, conflict semantics, credential boundaries and recovery across installations. Do not promise sync from a migration workflow.

## A website can come later

| Option | What it adds | Main cost |
| --- | --- | --- |
| Skill and GitHub README | Natural-language intake, access to local files, adaptive mapping and verification. | Depends on a capable agent and needs compatibility evaluation. |
| Documentation site | Installation help, examples and a tested compatibility matrix. | Low ongoing value unless documentation grows. |
| Browser-only archive inspector | A visual inventory and mapping preview without a server upload. | Large ZIP/Zstandard/SQLite processing, browser filesystem limits, and no automatic safe access to the live app. |
| Local desktop application | More controlled file access and a guided migration flow. | Packaging, signing, updates and a maintained migration engine. |

Start without a website. If users struggle with the mapping step, prototype a local browser inspector that generates a reviewed plan or portable archive. Do not imply that selecting an OS pair is enough to merge an active Codex database safely.

For any future browser product, verify local-only behavior in implementation: no analytics or third-party scripts that receive archive content, no archive upload endpoints, bounded streaming processing, and explicit handling of encrypted archives and unsupported formats. An empty upload server alone does not prove privacy. No website is implemented in this repository.

## Repository metadata

Recommended repository name: **`codex-migration-kit`**

Suggested GitHub description:

> A Codex skill for moving local chats, sessions, and custom skills between Windows and macOS, with project path mapping and recoverable merges.

Alternative names: `codex-device-migration` for search clarity, or `codex-carry` for a shorter brand. GitHub names are scoped by owner; these suggestions are not a claim of global uniqueness or trademark availability.

Suggested topics: `codex`, `agent-skills`, `migration`, `backup`, `windows`, `macos`, `local-first`.

## Launch presentation

Lead with the problem and one example prompt. Follow with installation, what transfers, exclusions, tested-versus-unverified directions, privacy, and recovery. Use synthetic examples for any screenshots or demo recording. Add a short visual demo only after the reusable flow has been exercised; avoid presenting a mockup as a working importer.

Tag an experimental release before describing it as stable. Ship the skill folder and its references together. A future plugin wrapper is reasonable if distribution needs it; OpenAI's current docs use plugins for reusable distribution. A standalone skill remains useful for local authoring and manual installation.

Existing projects such as Codex ReHome and Codex Session Transfer establish that this problem has other solutions. Position this kit around transparent assisted migration and compatibility evidence, and link related work in the README. Do not claim first-mover status or compete on unsupported "works with everything" promises.
