# Deep Research skill

An opencode agent skill that coordinates multi-source research and synthesizes it into a narrative report. It decomposes a question, spawns parallel research subagents with opencode's `task` tool, optionally runs one gap-filling round, then spawns a report writer.

Built and verified against opencode 1.18.3.

## Install into opencode

Clone this repo so that `SKILL.md` lands inside a skills directory that opencode scans. Clone it into a folder named `deep-research`. Do not clone it as `deep-research-skill`, because opencode requires the skill name and its containing folder name to match.

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

Restart opencode or start a new session so the skill is discovered. Verify it with

```
opencode debug skill
```

and look for `"name": "deep-research"` in the output. The `location` field should point at the clone.

## Use in opencode

There are three ways to start a run.

- Automatic. Ask a research question and the agent can load the skill from its description.
- Direct. Type `/deep-research <question>` and submit. opencode 1.18.3 registers skills as commands, so this resolves even though the slash autocomplete only lists `/skills`.
- Browse. Type `/skills`, pick `deep-research`, and add your question.

The skill writes `research_notes/<title>/` and `reports/<title>.md` under the current project directory. opencode has no file-send tool, so the final message gives you the absolute path to the report.

## Requirements

- opencode with the `task` tool and the built-in `general` subagent. Both ship with opencode.
- A web search provider for discovery. `websearch` is available with the OpenCode or OpenCode Go provider, or with `OPENCODE_ENABLE_EXA=1`. Without it, researchers can fall back to `webfetch` and `bash`, but results will be narrower.

## Update

```
git -C <install path> pull
```

## Contents

- `SKILL.md` holds the coordinator workflow
- `references/researcher.md` is read first by each research subagent
- `references/report-writer.md` is read first by the report writer subagent

## Notes

- The skill spawns parallel subagents with opencode's `task` tool and `subagent_type="general"`. It does not use `general-purpose`, which is a Claude Code agent name, and it does not pass `run_in_background`.
- To use the skill in Claude Code instead, replace `task` with `Agent`, `general` with `general-purpose`, `question` with `AskUserQuestion`, `websearch` with `WebSearch`, `webfetch` with `WebFetch`, `todowrite` with `TodoWrite`, and `write`/`read` with `Write`/`Read` in `SKILL.md` and the two reference files.
