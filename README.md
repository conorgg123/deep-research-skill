# Deep Research skill

An agent skill that coordinates multi-source research and synthesizes it into a narrative report. It decomposes a question, spawns parallel research subagents, optionally runs one gap-filling round, then spawns a report writer.

## Install into opencode

Clone this repo so that `SKILL.md` lands inside a skills directory that opencode scans. The containing folder must be named `deep-research`.

Global opencode config (available in every project)

macOS and Linux

```
git clone https://github.com/conorgg123/deep-research-skill.git ~/.config/opencode/skills/deep-research
```

Windows PowerShell

```
git clone https://github.com/conorgg123/deep-research-skill.git "$env:USERPROFILE\.config\opencode\skills\deep-research"
```

Claude-compatible location (also scanned by opencode)

macOS and Linux

```
git clone https://github.com/conorgg123/deep-research-skill.git ~/.claude/skills/deep-research
```

Windows PowerShell

```
git clone https://github.com/conorgg123/deep-research-skill.git "$env:USERPROFILE\.claude\skills\deep-research"
```

Restart opencode or start a new session so the skill is discovered. It then appears in the skill list as `deep-research` and loads on demand, either automatically when a research request matches it or manually by exact name.

## Update

```
git -C <install path> pull
```

## Contents

- `SKILL.md` holds the coordinator workflow
- `references/researcher.md` is read first by each research subagent
- `references/report-writer.md` is read first by the report writer subagent

## Notes

- The skill spawns parallel subagents, so the host must expose a Task or Agent tool.
- It asks subagents for `subagent_type="general-purpose"`. If your host names that type differently, for example `general`, edit that value in `SKILL.md`.
- Reports land in `reports/` and working notes in `research_notes/` under the host's project directory.
