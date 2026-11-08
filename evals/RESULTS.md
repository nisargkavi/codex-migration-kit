# Evaluation results

Evaluated on 8 November 2026 with an independent agent using disposable synthetic artifacts on macOS. The evaluator received the skill, the user request and the permitted artifact locations. It did not receive the expected answer or access the user's real Codex home.

These are behavioral dry-runs, not actual-device import certification. Fixture construction and evaluator scratch files were kept outside the repository. No actual user backup is distributed.

| Evaluation | Observed result | Preservation |
| --- | --- | --- |
| Windows backup inspection with committed WAL activity | Found both source records, including the WAL-only record; recognized one plain and one Zstandard-compressed session; identified the ambiguous project rename and a portable skill resource-link update. | Backup ZIP, destination database and copied project metadata hashes were unchanged; no destination WAL/SHM files were added. |
| Archive containing a traversal member | Rejected `../outside.txt` before extraction; did not open the member payload or attempt import. | Archive and destination database hashes and destination file inventory were unchanged. |

For the first case, the agent excluded the synthetic credential file and archived instructions without opening or extracting them. It did not execute imported code or access the network. It correctly reported that the minimal fixture had metadata-only sessions and insufficient version/history information to establish end-to-end Codex compatibility.

The ZIP traversal check covers one unsafe-member variant. Symlink escapes, expansion-limit enforcement, filesystem collision handling and other conditions in `cases.json` still require their own executed fixtures. The remaining import, cross-platform, idempotency, offline-apply and rollback scenarios are specified but have not been run for this reusable package.

Review also identified and clarified read-only filesystem probing, compressed-reference resolution, and the limits of structural compatibility evidence. The README installation instructions were reviewed separately for workspace-path ambiguity and corrected.

The precursor Windows → macOS migration informs the skill's technical guidance. It must not be counted as an end-to-end run of this new reusable skill.

## Published install command

The exact README command was executed successfully from the public GitHub repository on macOS with Node.js v26.13.0 and Skills CLI 1.7.6. It used a fresh temporary npm cache, a redirected Node home-directory API and a macOS sandbox denying writes outside the temporary test directory. A negative probe verified outside-write denial and denied reads of the real Codex configuration before installation.

The CLI found and installed one skill to the isolated `.agents/skills/codex-migrate` directory. All six installed files matched repository hashes, including the three references, display metadata and license. Before/after checks of 375 current configuration, credential and skill entries were identical. No GitHub credentials were inherited and telemetry was disabled. This was an isolated directory test, not a fresh OS VM or a Windows execution test.

After the publisher metadata update, a second fresh, protected install verified the changed skill files with the same successful preservation and file-matching checks. This run used the CLI's default telemetry to initiate the requested directory discovery; public-source audit and telemetry requests returned HTTP 200. The skills.sh skill page subsequently displayed the real instructions and install command. Neither test accessed real Codex data from inside the installer sandbox.
