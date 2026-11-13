# Claim Verification Pipeline

> Part of the NukoTech open skill set ([github.com/NukoTech](https://github.com/NukoTech)). MIT licensed. (c) 2026 Nuko Technologies LLC.

## What it is

Six-layer automated claim verification: corpus construction, entity and claim extraction, intra-document consistency, cross-source triangulation, external signal corroboration, hypothesis matrix. Domain-agnostic. Activate when evaluating technical claims, performing due diligence, assessing vendor claims, or verifying research findings. Triggers: is this claim true, verify this, due diligence, fact check, evaluate this technology.

## Install


```bash
git clone https://github.com/NukoTech/claim-verification-pipeline.git
```


Copy the skill folder into your agent's skills directory (for example `~/.claude/skills/` for Claude Code, or your platform's equivalent). Each `SKILL.md` has YAML front matter (`name`, `description`) that agent runtimes use to decide when to load it.

## Usage

Ask your agent for the task described above; the runtime loads the skill when the request matches its description. You can also paste the main file into a system prompt or custom-instructions field.

## Files

- `SKILL.md`

## Contributing

See `CONTRIBUTING.md`. Fork and open a pull request; maintainer review is required.

## License

MIT. Copyright (c) 2026 Nuko Technologies LLC. See `LICENSE`.
