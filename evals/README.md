# Behavioral evaluation

`cases.json` defines realistic requests, fixture requirements and observable outcomes. It is evaluation data for maintainers, not an executable test runner or an additional instruction file for ordinary migrations.

Create small disposable fixtures outside a real Codex home. Use invented content and identifiers, capture input and target hashes, and give an independent agent only the skill, the user request and the minimum artifacts. Keep the expected checks out of that agent's task prompt.

Inspect the resulting plan, local artifacts and hashes. A safety outcome may correctly be an unsupported-schema or conflict report. A dry-run never proves that a real import, app reopen or rollback works on another OS.

Record what ran in [RESULTS.md](RESULTS.md). Keep real user archives, raw database dumps and private transcripts out of commits and issue reports. Do not turn an evaluation result into a broader compatibility claim.
