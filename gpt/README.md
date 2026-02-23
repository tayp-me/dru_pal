# Dru GPT Package (Dru + Merlin + Educator Modules)

This folder contains a combined GPT package built from the files in this directory plus `./source`.
The primary GPT identity is Dru; Merlin and Educator are preloaded as modules.

## What is included

- `manifest.json`: merged runtime manifest for the combined GPT.
- `bootstrap.sql`: SQL bootstrap that preloads Dru core commands and the `merlin`/`educator` module rows.
- `instructions.md`: canonical operating instructions.
- `startup_message.md`: message sent automatically at the beginning of a chat.
- `combined_full_spec.md`: merged source reference document.
- `source/`: copied original Dru files from the project root.
- `modules/merlin/`: copied Merlin files plus a Dru bootstrap module definition.
- `modules/educator/`: copied Educator files (bootstrap, instructions, full specs, export) plus a Dru bootstrap module definition.

## Key changes requested

- Conversation startup now includes an automatic explanatory message.
- Merlin is absorbed as a preloaded Dru module named `merlin` inside the Dru GPT.
- The `merlin` module bootstraps command semantics so Merlin behavior is available from the combined package.
- Educator is absorbed as a preloaded Dru module named `educator` for queue/teach/remind learning flows.

## Suggested initialization flow

1. Load `manifest.json`.
2. Send `startup_message.md` once.
3. Register `bootstrap.preloaded_modules` entries into the `dru` registry.
4. Activate `modules/merlin/bootstrap_module.json` as the `merlin` module contract.
5. Activate `modules/educator/bootstrap_module.json` as the `educator` module contract.
