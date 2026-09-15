# Agent Skills

A small, growing collection of reusable agent skills for Codex, Claude Code, and
other agents that support the `SKILL.md` convention.

Each directory at the repository root is one independent skill. Skills contain
instructions an agent can load when a task matches their purpose.

## Available skills

| Skill | Purpose |
| --- | --- |
| [auto-compact](auto-compact/SKILL.md) | Creates a structured session checkpoint that preserves decisions, constraints, state, errors, and next steps during long-running work. |
| [task-breakdown](task-breakdown/SKILL.md) | Turns compound prompts into a concise task table, tracks dependencies and acceptance criteria, and reports only changed items during execution. |

## Install a skill

Clone this repository, then copy the skill directory you want into your agent's
personal skills location.

The examples below install `auto-compact`. To install `task-breakdown`, replace
`auto-compact` with `task-breakdown` in the source and destination paths.

```powershell
git clone https://github.com/ReBioNC/agentskill.git
```

### Codex

Copy the skill folder to your personal Codex skills directory:

```powershell
Copy-Item -Recurse .\agentskill\auto-compact "$env:USERPROFILE\.agents\skills\auto-compact"
```

Restart Codex if the skill does not appear automatically. Invoke it with:

```text
$auto-compact
```

### Claude Code

Copy the skill folder to your personal Claude Code skills directory:

```powershell
Copy-Item -Recurse .\agentskill\auto-compact "$env:USERPROFILE\.claude\skills\auto-compact"
```

Restart Claude Code if necessary. Invoke it with:

```text
/auto-compact
```

## Task Breakdown usage

For a task table only, use `$task-breakdown` in Codex or `/task-breakdown` in
Claude Code, followed by your request:

```text
$task-breakdown
Fix upload retries, update the README, and investigate slow staging.
Do not deploy. After retry tests pass, draft an Indonesian release note
under 90 words.
```

Add `Then execute the ready tasks` to authorize execution after the breakdown.
Use `$task-breakdown refresh` (or `/task-breakdown refresh`) with new instructions
to update the existing task IDs. Ask to `show the full table` when you need a
complete view; routine updates include only changes.

The skill is self-contained in `task-breakdown/SKILL.md`, with no required scripts
or supporting files. Short instructions, one row per outcome, and updates only
when something changes limit overhead; actual token usage depends on the session.
