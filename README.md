# Teaching Programming Skill

`teaching-programming` is an instruction-only skill for coding sessions where the user wants to learn while the agent implements.

It turns the assistant into a step-by-step programming teacher: make a small change, show the change, explain the reason, then continue.

## Status

Current version: `0.1.0`

This is the first public version of the skill. It is ready to test and iterate on, but the instructions may continue evolving based on real usage.

Release notes for published versions live in [`CHANGELOG.md`](./CHANGELOG.md).

## Ownership and license

Copyright (c) 2026 Sergio Alonso.

Licensed under `AGPL-3.0-or-later`. See [`LICENSE`](./LICENSE).

## Quick path

1. Install `SKILL.md` under a skill folder named `teaching-programming`.
2. Ask the agent to teach while coding, for example: `Enseñame mientras agregas validación a esta función.`
3. Verify that the agent switches to small teaching steps instead of dumping a full solution.

## What this skill enforces

When active, the assistant must:

- work in small teaching steps
- stop after meaningful logic changes
- show the full absolute file path for every modified file
- show a contextual diff whenever possible
- include 5 lines before and 5 lines after the changed region whenever possible
- explain what changed, why it changed, the programming concept involved, and what would happen otherwise
- end with a short learning summary

It should also:

- ask before leaving teaching mode for a faster implementation mode
- reduce explanations of basic syntax once the user clearly understands it
- preserve correctness and avoid oversized rewrites

## Good trigger examples

Spanish:

- `enseñame`
- `enséñame`
- `explicame mientras programas`
- `explícame mientras programas`
- `paso a paso`
- `modo enseñanza`

English:

- `teach me`
- `step by step`
- `explain while coding`
- `teaching mode`
- `walk me through it`

## Expected behavior

If the user says:

```text
Enseñame mientras agregas validación a esta función.
```

the assistant should:

1. activate teaching mode
2. change one meaningful part first
3. show the full file path
4. show the changed region with surrounding context
5. explain the change before moving on

## Repository contents

```text
learn-by-coding-skill/
├── CHANGELOG.md
├── .gitignore
├── LICENSE
├── README.md
└── SKILL.md
```

Notes:

- `SKILL.md` is the canonical runtime instruction file.
- `README.md` explains intent, installation, and verification.
- `CHANGELOG.md` tracks published release history.
- `.atl/` is treated as local environment state and is intentionally excluded from the published repo.

## Canonical skill name

Use this exact folder name when installing the skill:

```text
teaching-programming
```

## Installation

The portable rule is simple: place `SKILL.md` inside a folder named `teaching-programming` wherever your agent discovers skills.

### OpenCode

If your OpenCode setup discovers skills from standard project or global skill folders, this is the expected layout:

Project-local:

```bash
mkdir -p .opencode/skills/teaching-programming
cp SKILL.md .opencode/skills/teaching-programming/SKILL.md
```

Global:

```bash
mkdir -p ~/.config/opencode/skills/teaching-programming
cp SKILL.md ~/.config/opencode/skills/teaching-programming/SKILL.md
```

### Claude-style skill folders

For Claude-style skill folders, this is a common layout:

Project-local:

```bash
mkdir -p .claude/skills/teaching-programming
cp SKILL.md .claude/skills/teaching-programming/SKILL.md
```

Global:

```bash
mkdir -p ~/.claude/skills/teaching-programming
cp SKILL.md ~/.claude/skills/teaching-programming/SKILL.md
```

### AGENTS.md-based tools

If your tool does not auto-discover `SKILL.md`, keep the skill in a project folder and reference it from `AGENTS.md` or an equivalent instruction file.

```bash
mkdir -p .agents/skills/teaching-programming
cp SKILL.md .agents/skills/teaching-programming/SKILL.md
```

Then point your `AGENTS.md` instructions to:

```text
.agents/skills/teaching-programming/SKILL.md
```

### Direct path loading

If your agent supports passing a skill path directly, keep the file somewhere stable:

```bash
mkdir -p ~/ai-skills/teaching-programming
cp SKILL.md ~/ai-skills/teaching-programming/SKILL.md
```

Then load:

```text
~/ai-skills/teaching-programming/SKILL.md
```

## Recommended project layout

```text
my-project/
├── AGENTS.md
├── .agents/
│   └── skills/
│       └── teaching-programming/
│           └── SKILL.md
├── .opencode/
│   └── skills/
│       └── teaching-programming/
│           └── SKILL.md
└── .claude/
    └── skills/
        └── teaching-programming/
            └── SKILL.md
```

You do not need every copy unless you want broad compatibility.

## Verification prompt

After installing, test with:

```text
Enseñame mientras creas una función simple que reciba una lista de números y devuelva la suma de los números pares. Detente después de crear la función, después del bucle y después del if.
```

Expected outcome:

- the agent recognizes teaching mode
- it avoids a single large unexplained solution
- it shows file paths and contextual diffs
- it explains the function, the loop, and the condition
- it ends with a short learning summary

## Scope and limits

- This is an instruction-only skill.
- It does not execute code or install dependencies by itself.
- It is safe to inspect because its behavior is defined in plain Markdown.
- The runtime source of truth is `SKILL.md`.
- Tool-specific discovery behavior can vary, so verify exact paths and loading rules in your chosen agent before wider rollout.
