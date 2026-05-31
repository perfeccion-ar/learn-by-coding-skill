# Teaching Programming Skill

`teaching-programming` is an instruction-only agent skill for educational coding sessions.

It makes the coding assistant slow down and teach while it writes or modifies code. When active, the assistant must stop after each meaningful programming construct, show the modified lines, and explain the reason for the change.

The skill is written in English, but it activates from both Spanish and English trigger phrases.

## What it does

When the user says something like:

- `enseñame`
- `enséñame`
- `educame`
- `edúcame`
- `explicame`
- `explícame`
- `paso a paso`
- `modo enseñanza`
- `teach me`
- `educate me`
- `step by step`
- `teaching mode`
- `explain while coding`

…the agent should enter teaching mode.

While in teaching mode, the agent must:

1. Make small code changes instead of large unexplained edits.
2. Stop after creating or modifying a function, loop, conditional, class, exception handler, database query, network request, file operation, or other meaningful logic block.
3. Show the changed lines, preferably as a compact diff.
4. Explain what changed.
5. Explain why the change was necessary.
6. Explain the programming concept involved.
7. Explain what would happen if the change were not made.
8. End the task with a short learning summary.

## Files included

```text
teaching-programming-skill/
├── README.md
└── SKILL.md
```

## Skill name

The canonical skill name is:

```text
teaching-programming
```

Use this same directory name when installing it into tools that discover skills from folders.

---

# Installation

Different coding agents discover custom instructions in different ways. Some support `SKILL.md` directly. Others use context files such as `AGENTS.md`, `CLAUDE.md`, or explicit command-line flags.

The recommended portable layout is to keep this repository or folder somewhere stable, for example:

```bash
mkdir -p ~/ai-skills/teaching-programming
cp SKILL.md README.md ~/ai-skills/teaching-programming/
```

Then install or link it into the tool-specific location you use.

---

## OpenCode

OpenCode supports agent skills through `SKILL.md` files.

OpenCode discovers skills from several locations, including project-local and global folders:

- Project: `.opencode/skills/<name>/SKILL.md`
- Global: `~/.config/opencode/skills/<name>/SKILL.md`
- Claude-compatible project: `.claude/skills/<name>/SKILL.md`
- Claude-compatible global: `~/.claude/skills/<name>/SKILL.md`
- Agent-compatible project: `.agents/skills/<name>/SKILL.md`
- Agent-compatible global: `~/.agents/skills/<name>/SKILL.md`

### Project-local install

From your project root:

```bash
mkdir -p .opencode/skills/teaching-programming
cp SKILL.md .opencode/skills/teaching-programming/SKILL.md
```

### Global install

```bash
mkdir -p ~/.config/opencode/skills/teaching-programming
cp SKILL.md ~/.config/opencode/skills/teaching-programming/SKILL.md
```

### Test in OpenCode

Open your project with OpenCode and ask:

```text
Enseñame mientras agregas validación a esta función.
```

or:

```text
Teach me while you refactor this function step by step.
```

---

## Claude Code / claude CLI

Claude Code supports skills through `SKILL.md` files.

Typical locations are:

- Personal/global: `~/.claude/skills/<skill-name>/SKILL.md`
- Project-local: `.claude/skills/<skill-name>/SKILL.md`

### Personal/global install

```bash
mkdir -p ~/.claude/skills/teaching-programming
cp SKILL.md ~/.claude/skills/teaching-programming/SKILL.md
```

### Project-local install

From your project root:

```bash
mkdir -p .claude/skills/teaching-programming
cp SKILL.md .claude/skills/teaching-programming/SKILL.md
```

### Test in Claude Code

Start Claude Code from the project:

```bash
claude
```

Then ask:

```text
/teaching-programming
```

or use a natural trigger:

```text
Enseñame paso a paso mientras implementas esta función.
```

---

## Codex CLI

Codex CLI primarily uses `AGENTS.md` files for persistent custom instructions. It may not load `SKILL.md` as an automatic skill in the same way as OpenCode or Claude Code.

Recommended installation for Codex is to keep the skill file in your repository and reference it from `AGENTS.md`.

### Project-local install

From your project root:

```bash
mkdir -p .agents/skills/teaching-programming
cp SKILL.md .agents/skills/teaching-programming/SKILL.md
```

Then create or edit `AGENTS.md`:

```bash
cat >> AGENTS.md <<'EOF_AGENTS'

## Teaching Programming Skill

When the user says "enseñame", "enséñame", "educame", "edúcame", "explicame", "explícame", "paso a paso", "modo enseñanza", "teach me", "educate me", "step by step", or "teaching mode", follow the instructions in:

`.agents/skills/teaching-programming/SKILL.md`

In this mode, make small code changes, stop after each function, loop, conditional, or meaningful logic change, show the modified lines, and explain why the change was made.
EOF_AGENTS
```

### Global install

```bash
mkdir -p ~/.codex/skills/teaching-programming
cp SKILL.md ~/.codex/skills/teaching-programming/SKILL.md
mkdir -p ~/.codex
cat >> ~/.codex/AGENTS.md <<'EOF_AGENTS'

## Teaching Programming Skill

When the user says "enseñame", "enséñame", "educame", "edúcame", "explicame", "explícame", "paso a paso", "modo enseñanza", "teach me", "educate me", "step by step", or "teaching mode", follow the instructions in:

`~/.codex/skills/teaching-programming/SKILL.md`

In this mode, make small code changes, stop after each function, loop, conditional, or meaningful logic change, show the modified lines, and explain why the change was made.
EOF_AGENTS
```

### Test in Codex

From a project directory:

```bash
codex "Enseñame mientras agregas validación a esta función."
```

---

## Google Antigravity CLI / Antigravity

Google Antigravity supports instruction-only skills using `SKILL.md`.

The documented global skill path is:

```text
~/.gemini/antigravity/skills/<skill-name>/SKILL.md
```

Antigravity also supports workspace skills under:

```text
.agents/skills/<skill-name>/SKILL.md
```

### Global install

```bash
mkdir -p ~/.gemini/antigravity/skills/teaching-programming
cp SKILL.md ~/.gemini/antigravity/skills/teaching-programming/SKILL.md
```

### Workspace install

From your project root:

```bash
mkdir -p .agents/skills/teaching-programming
cp SKILL.md .agents/skills/teaching-programming/SKILL.md
```

### Test in Antigravity

Ask the agent:

```text
Enseñame mientras refactorizas esta función paso a paso.
```

or:

```text
Teach me while you add error handling to this script.
```

---

## Pi coding agent

Pi supports skills and can load them explicitly with the `--skill <path>` option. Pi also supports context files such as `AGENTS.md` and `CLAUDE.md`.

### Direct skill loading

Keep the skill in a stable location:

```bash
mkdir -p ~/ai-skills/teaching-programming
cp SKILL.md ~/ai-skills/teaching-programming/SKILL.md
```

Run Pi with the skill:

```bash
pi --skill ~/ai-skills/teaching-programming/SKILL.md "Enseñame mientras mejoras esta función."
```

You can repeat `--skill` for multiple skills.

### Project-local install with AGENTS.md

From your project root:

```bash
mkdir -p .agents/skills/teaching-programming
cp SKILL.md .agents/skills/teaching-programming/SKILL.md
cat >> AGENTS.md <<'EOF_AGENTS'

## Teaching Programming Skill

When the user says "enseñame", "enséñame", "educame", "edúcame", "explicame", "explícame", "paso a paso", "modo enseñanza", "teach me", "educate me", "step by step", or "teaching mode", follow the instructions in:

`.agents/skills/teaching-programming/SKILL.md`

In this mode, make small code changes, stop after each function, loop, conditional, or meaningful logic change, show the modified lines, and explain why the change was made.
EOF_AGENTS
```

### Test in Pi

```bash
pi --skill .agents/skills/teaching-programming/SKILL.md "Teach me while you implement this loop."
```

Inside the interactive UI, Pi skills are available through slash commands using the `/skill:name` form when loaded by the tool.

---

# Recommended cross-tool project layout

For a repository that may be used by multiple agents, this layout is practical:

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

You do not need all three copies unless you want maximum compatibility.

A simple approach is to store the real file once and use symbolic links:

```bash
mkdir -p .agents/skills/teaching-programming
cp SKILL.md .agents/skills/teaching-programming/SKILL.md

mkdir -p .opencode/skills .claude/skills
ln -s ../../.agents/skills/teaching-programming .opencode/skills/teaching-programming
ln -s ../../.agents/skills/teaching-programming .claude/skills/teaching-programming
```

If symbolic links cause trouble on your platform, copy the file instead.

---

# Quick verification prompt

After installing, test with this prompt:

```text
Enseñame mientras creas una función simple que reciba una lista de números y devuelva la suma de los números pares. Detente después de crear la función, después del bucle y después del if.
```

Expected behavior:

- The agent should recognize teaching mode.
- It should not dump a large unexplained solution.
- It should show changed lines.
- It should explain the function.
- It should explain the loop.
- It should explain the `if` condition.
- It should end with a short learning summary.

---

# Notes

- This is an instruction-only skill. It does not run scripts or install dependencies.
- It is safe to inspect because all behavior is defined in plain Markdown.
- For tools without native `SKILL.md` discovery, use `AGENTS.md` as the compatibility bridge.
- Keep the skill name lowercase and hyphenated: `teaching-programming`.
