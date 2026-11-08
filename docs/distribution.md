# Distribution and directory discovery

Reviewed 8 November 2026. Directory inclusion, search indexing and ranking are separate from a successful installation. This document records supported routes; it does not claim that a submission has been accepted.

## skills.sh

[Vercel's FAQ](https://www.skills.sh/docs/faq) says listing is driven by aggregated telemetry from normal `skills add` installs. There is no separate submission form in that documented route. Public install metrics and cached directory processing can take time; do not manufacture installs or claim a ranking.

Use the one-line command in the README. The supported `skills/codex-migrate/SKILL.md` layout and required frontmatter are already present. There is no need to duplicate SKILL.md at the repository root or add a plugin manifest just for CLI discovery. See [Vercel's skill creation guidance](https://github.com/vercel-labs/skills/blob/main/docs/creating-skills.md).

The repository includes a repository-hosted SVG badge linked to the live skill page and a `skills.sh.json` grouping configuration. The dynamic install-count badge endpoint failed for this repository and a Vercel reference repository during checking, so the README uses a local asset without claiming an install count. [Customization documentation](https://www.skills.sh/docs/customize) says configuration is refreshed after a telemetry-enabled install and can remain cached temporarily. This display configuration does not register a skill by itself.

Verified directory page: https://skills.sh/nisargkavi/codex-migration-kit/codex-migrate

Status: the public skill page was verified live on 8 November 2026, showing the install command and our actual skill instructions. After publishing the metadata update, one isolated install of that updated package used the CLI's default telemetry; its telemetry and audit endpoints returned HTTP 200. This is not a claim about search placement, install counts or leaderboard rank. The initial installer test disabled telemetry and did not initiate indexing.

The directory currently displays passing Agent Trust Hub and Socket checks and a [Snyk W011 warning](https://skills.sh/nisargkavi/codex-migration-kit/codex-migrate/security/snyk) about exposure to untrusted archive content. See SECURITY.md for scope and mitigations; do not present the listing as unanimous security approval.

## SkillsMP

[SkillsMP's own About page](https://skillsmp.com/about) describes collecting SKILL.md files from public GitHub repositories. Our public, correctly structured skill is suitable for that discovery route, but no crawler schedule or guaranteed inclusion was established.

Status: public source is ready for crawling; catalog inclusion is unconfirmed. We have not sent support email, paid for promotion, or claimed a listing. Recheck by repository URL or `codex-migrate` after the catalog refreshes.

## Skills Directory

[Skills Directory](https://www.skillsdirectory.com/) offers a reviewed submission flow. Its [submission page](https://app.skillsdirectory.com/submit) redirects to sign-in and supports GitHub, Google or email sign-in.

Status: submission metadata is prepared below; no account connection or submission has been completed. Sign in as the repository owner, review any requested access and terms, and submit the public skill source. A submission is not approval.

## Reusable listing information

- **Display name:** Codex Migration Kit
- **Skill identifier:** `codex-migrate`
- **Publisher:** `nisargkavi`
- **Repository:** https://github.com/nisargkavi/codex-migration-kit
- **Skill source:** https://github.com/nisargkavi/codex-migration-kit/tree/main/skills/codex-migrate
- **Raw instructions:** https://raw.githubusercontent.com/nisargkavi/codex-migration-kit/main/skills/codex-migrate/SKILL.md
- **Category:** Developer tools / agent workflows / migration and backup
- **Description:** An assisted Codex skill for inspecting, exporting and merging available local chats, sessions and custom skills across Windows and macOS, with project mapping and recovery guidance.
- **License:** MIT
- **Maturity:** Experimental; cross-platform workflow guidance with limited actual-device evidence.

List the public instructions and documentation, never real backup archives, private transcripts or credentials. Do not describe the skill as continuous sync, fully offline, or universally compatible.
