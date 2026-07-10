# spec-forge

A Claude Code plugin that turns a natural-language feature or project idea into
a **spec-driven-development (SDD)** specification:

- **`requirements.md`** — the *what*, written in [EARS](skills/spec-forge/references/ears-notation.md) notation
- **`design.md`** — the *how*, the technical design

It asks **only the essential clarifying questions** when your prompt is vague,
reviews requirements with you before designing, and **never generates code** —
it stops at design.

## Install

Inside a Claude Code session:

```
/plugin marketplace add andressa-soares/spec-forge-plugin
/plugin install spec-forge@sdd
```

Or from the CLI:

```bash
claude plugin marketplace add andressa-soares/spec-forge-plugin
claude plugin install spec-forge@sdd
```

`spec-forge@sdd` reads as `plugin@marketplace` — the `spec-forge` plugin from the
`sdd` marketplace.

## Usage

The skill is **model-invoked**: just describe what you want to build and Claude
triggers it automatically from its description. A vague prompt is fine — the
skill will ask what it genuinely needs:

> Quero fazer um app de lista de tarefas com lembretes.

To invoke it explicitly, use the namespaced slash command (`plugin:skill`):

```
/spec-forge:spec-forge
```

Either way, the skill runs a small state machine: clarify → generate
`requirements.md` → **review checkpoint** → clarify the tech → generate
`design.md`, writing both files to `specs/<feature-name>/`.

## What's inside

```
.claude-plugin/
  plugin.json          # plugin manifest
  marketplace.json     # single-plugin marketplace manifest (name: sdd)
skills/
  spec-forge/
    SKILL.md           # the skill definition (state machine + guardrails)
    assets/            # requirements & design templates
    references/        # EARS notation reference
```

The skill writes its output to `specs/<feature-name>/` in your own project;
that directory is not part of the published plugin.

## Local development

To try changes before pushing, add this checkout as a local marketplace:

```
/plugin marketplace add ./
/plugin install spec-forge@sdd
```

After editing files, refresh with `/plugin marketplace update sdd`.

## License

[MIT](LICENSE) © Andressa
