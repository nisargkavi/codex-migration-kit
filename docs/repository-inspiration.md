# Repository examples and presentation choices

These are primary-source examples, not a measured ranking by stars. Repositories and documentation were reviewed on 8 November 2026.

| Repository | Observed pattern | Applied here |
| --- | --- | --- |
| [Agent Skills](https://github.com/agentskills/agentskills) | Portable skill format and progressive disclosure. | Short routing instructions with conditional references. |
| [Anthropic Skills](https://github.com/anthropics/skills) | Self-contained skill folders, a small frontmatter template and usage examples. | A complete installable folder and concrete export/import prompts. |
| [Vercel Agent Skills](https://github.com/vercel-labs/agent-skills) | Clear use cases, discoverable installation, small focused skills and supporting resources. | Problem-first README, explicit triggers and a compact repository map. |
| [OpenAI Plugins](https://github.com/openai/plugins) | Current OpenAI packaging examples with skills and optional connector surfaces. | Codex UI metadata today, with a possible plugin wrapper when distribution needs it. |
| [OpenAI Skills](https://github.com/openai/skills) | Historical examples; its current README directs readers to plugins. | Historical reference only, not the current distribution recommendation. |

The [Anthropic template](https://github.com/anthropics/skills/blob/main/template/SKILL.md) and [Vercel web-design-guidelines skill](https://github.com/vercel-labs/agent-skills/blob/main/skills/web-design-guidelines/SKILL.md) are useful small examples to read before adding more structure.

The README includes a compatibility matrix and privacy explanation because this skill handles valuable local history. Contributor and issue templates ask for synthetic evidence because real backup files are unsuitable for public debugging.

## Related migration tools

- [Codex ReHome](https://github.com/CalebYcj/codex-rehome) and its [skill](https://github.com/CalebYcj/codex-rehome-skill) are directly related cross-device migration projects.
- [Codex Session Transfer](https://github.com/myyimu/codex-session-transfer) is another local export/import project.

These projects establish prior work. This kit's intended value is a concise, inspectable, agent-guided workflow and explicit compatibility evidence. The instructions and documentation here were written for this package; referencing a repository does not grant permission to copy its licensed assets or implementation without observing its license.
