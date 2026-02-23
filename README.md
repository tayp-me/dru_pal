# Dru + Merlin GPT Package Repository

## GPT Link
[Dru Pal on ChatGPT](https://chatgpt.com/g/g-68370be35e2c81919744a05c8629fbb5-dru-pal)

## What this project is
This repository contains source material and packaged artifacts for a custom GPT system built around:

- **Dru**: the primary assistant identity, designed as a command-driven, SQL-like module scaffolding system.
- **Merlin**: a secondary module that can be invoked from within Dru.

This is a **configuration/specification package**, not a conventional application codebase. Most files are manifests, instruction documents, specs, and bootstrap SQL used to assemble/import the GPT behavior.

## Repository structure

### Top-level

| Path | Type | Purpose |
| --- | --- | --- |
| `AGENTS.md` | file | Repository-level rules for scaffold-only outputs and no personal/historical data. |
| `README.md` | file | Project overview and structure reference. |
| `manifest.json` | file | Original Dru manifest (identity, commands, alias, schema, startup/import metadata). |
| `gpt.zip` | file | Archived export of the `gpt/` package directory. |
| `gpt/` | folder | Combined Dru + Merlin + Educator package ready for import/use. |

### `gpt/` (combined package)

| Path | Purpose |
| --- | --- |
| `gpt/manifest.json` | Merged runtime manifest for Dru with preloaded Merlin and Educator module support. |
| `gpt/instructions.md` | Canonical operating instructions for the combined package. |
| `gpt/startup_message.md` | One-time boot message text for new conversations. |
| `gpt/bootstrap.sql` | SQL bootstrap defining core `dru` table and preloaded command rows (including `merlin` and `educator`). |
| `gpt/combined_full_spec.md` | Consolidated full-package reference spec. |
| `gpt/README.md` | Package-specific overview and initialization notes. |
| `gpt/source/` | Snapshot of original source inputs used to produce the combined package. |
| `gpt/modules/merlin/` | Merlin module files plus Dru-compatible bootstrap mapping. |
| `gpt/modules/educator/` | Educator module files plus Dru-compatible bootstrap mapping. |

### `gpt/source/`

| Path | Purpose |
| --- | --- |
| `gpt/source/Dru_Extremely_Verbose_Combined.md` | Canonical long-form Dru architecture/specification reference source. |
| `gpt/source/dru_mod_export_addendum_no_flags.md` | Addendum source defining `mod export {{ name_machine }}` behavior. |
| `gpt/source/dru_conversation_log.md` | Conversation-log source used to derive module behavior. |
| `gpt/source/dru_module_educator_export.md` | Educator export source used for scaffold integration. |
| `gpt/source/merlin_instructions.txt` | Merlin instruction source file. |
| `gpt/source/merlin_full_conversation_spec.md` | Human-readable Merlin specification source. |
| `gpt/source/merlin_full_conversation_spec.yaml` | Machine-readable Merlin specification source. |
| `gpt/source/instructions_old.md` | Legacy Dru instruction source snapshot. |

### `gpt/modules/merlin/`

| Path | Purpose |
| --- | --- |
| `gpt/modules/merlin/bootstrap_module.json` | Module contract/mapping used to register Merlin semantics inside Dru. |
| `gpt/modules/merlin/merlin_instructions.txt` | Merlin instruction text scoped for module execution. |
| `gpt/modules/merlin/merlin_full_conversation_spec.md` | Human-readable technical specification for Merlin behavior. |
| `gpt/modules/merlin/merlin_full_conversation_spec.yaml` | Machine-readable Merlin behavior specification. |
| `gpt/modules/merlin/README.md` | Short module-level overview. |

### `gpt/modules/educator/`

| Path | Purpose |
| --- | --- |
| `gpt/modules/educator/bootstrap_module.json` | Module contract/mapping used to register Educator semantics inside Dru. |
| `gpt/modules/educator/educator_instructions.txt` | Educator module runtime instruction file (parallel to Merlin pattern). |
| `gpt/modules/educator/educator_full_conversation_spec.md` | Human-readable full technical spec for Educator behavior. |
| `gpt/modules/educator/educator_full_conversation_spec.yaml` | Machine-readable full technical spec for Educator behavior. |
| `gpt/modules/educator/educator_instructions.md` | Module behavior contract for queue/teach/remind/remove flows. |
| `gpt/modules/educator/dru_module_educator_export.md` | Canonical export source used for module integration. |
| `gpt/modules/educator/README.md` | Short module-level overview. |

## Suggested initialization flow (for the combined package)

1. Load `gpt/manifest.json`.
2. Send `gpt/startup_message.md` once at conversation start.
3. Apply/interpret `gpt/bootstrap.sql` to seed command registry and module rows.
4. Use `gpt/modules/merlin/bootstrap_module.json` to activate Merlin as a subordinate Dru module when explicitly targeted.
5. Use `gpt/modules/educator/bootstrap_module.json` to activate Educator as a subordinate Dru module when explicitly targeted.
