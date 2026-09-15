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

Replace the `skill-name` with the skill you want to install

```powershell
git clone https://github.com/ReBioNC/agentskill.git
```

### Codex

Copy the skill folder to your personal Codex skills directory:

```powershell
Copy-Item -Recurse .\agentskill\auto-compact "$env:USERPROFILE\.agents\skills\skill-name"
```

Restart Codex if the skill does not appear automatically. Invoke it with:

```text
$skill-name
```

### Claude Code

Copy the skill folder to your personal Claude Code skills directory:

```powershell
Copy-Item -Recurse .\agentskill\auto-compact "$env:USERPROFILE\.claude\skills\skill-name"
```

Restart Claude Code if necessary. Invoke it with:

```text
/skill-name
```