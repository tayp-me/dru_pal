# AGENTS.md

## Repository Rule: Skeleton Only

This repository is strictly for scaffolding and functionality definitions.
It must never store or scaffold historical/runtime data.

## Hard Requirements

- Never include historical data in committed files or generated scaffolds.
- Never include personal data of any kind (PII, sensitive details, user-specific content) in this repository.
- Never include personal data in anything this repository scaffolds or exports.
- Treat all outputs as skeletons: functionality only, no content payloads.

## Functional-Only Scaffolding

When building from source files (including `.md`, `.sql`, `.json`, `.yaml`, logs, or exports):

- Extract only functionality: command names, schema shape, interfaces, control flow, and behavior contracts.
- Do not copy data values, historical rows, examples, timestamps, user entries, notes, or conversation content.
- Replace all potential data payloads with empty structures or placeholders.

## SQL-Specific Rules

Allowed:

- `CREATE TABLE`, indexes, constraints, and command/registry structure.

Forbidden:

- Any seeded historical or personal rows.
- Any `INSERT` statements that add user/content/history data.
- Any copied data payload from source exports.

## Documentation and Module Rules

Allowed:

- API/module behavior descriptions and command semantics.
- Placeholder examples like `<concept>` or `<argument>`.

Forbidden:

- Real concepts, personal examples, logs, or historical snapshots.
- Any copied dataset from source markdown/SQL files.

## Enforcement

Before finalizing changes, verify:

1. No personal data exists in changed files.
2. No historical/runtime data is seeded.
3. Scaffolds are empty skeletons with functionality only.

If any source includes personal or historical data, redact/omit it and keep only structural/functionality definitions.

## Packaging Rule (Required After Any Change)

After making any repository change, rebuild `gpt.zip` from `./gpt` in ChatGPT import format.

- The zip root must be the contents of `./gpt` (for example `manifest.json`, `instructions.md`, `modules/...`), not a top-level `gpt/` folder wrapper.
- Always rebuild the zip fresh (do not append to an existing archive).

Recommended command:

`(cd gpt && zip -r ../gpt.new.zip .) && mv -f gpt.new.zip gpt.zip`
