# Agent Skills

A small, growing collection of reusable agent skills for Codex, Claude Code, and
other agents that support the `SKILL.md` convention.

Each directory at the repository root is one independent skill. Skills contain
instructions an agent can load when a task matches their purpose.

## Available skills

| Skill | Purpose |
| --- | --- |
| [auto-compact](auto-compact/SKILL.md) | Creates a structured session checkpoint that preserves decisions, constraints, state, errors, and next steps during long-running work. |

## Install a skill

Clone this repository, then copy the skill directory you want into your agent's
personal skills location.

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

## Add a new skill

Create one root-level folder per skill. A minimal skill needs only `SKILL.md`:

```text
my-skill/
└── SKILL.md
```

`SKILL.md` should start with YAML frontmatter that clearly describes what the
skill does and when an agent should use it:

```markdown
---
name: my-skill
description: Explain what this skill does and when to use it.
---

# My Skill

Instructions for the agent.
```

Use lowercase hyphenated names. Keep each skill self-contained and avoid putting
project-specific secrets, credentials, or task history in the repository.

## Repository layout

```text
agentskill/
├── README.md
├── auto-compact/
│   └── SKILL.md
└── <future-skill>/
    └── SKILL.md
```

Optional files such as `references/`, `scripts/`, `assets/`, or
`agents/openai.yaml` may live inside a skill directory when they directly support
that skill. They are not required for a minimal, portable skill.

## Using Auto-Compact

Use `$auto-compact` in Codex or `/auto-compact` in Claude Code when a session is
long, complex, or nearing its context limit. The skill prepares a checkpoint with
the important task facts. Native context replacement remains controlled by the
host's own compact command, such as `/compact`.
