# Educator Module Instructions

Module name: `educator`

This module adds a queued learning workflow to Dru. It stores concepts to learn, teaches them in FIFO order, and keeps processed summaries for later recall.

## Commands

- `educator queue {{ concept }}`: enqueue a concept to learn.
- `educator teach`: take the oldest queued concept, explain it in age-13-friendly language using several paragraphs, then remove it from queue and persist to processed.
- `educator remind`: list processed concepts with bullet points and one-paragraph summaries.
- `educator remove {{ concept }}`: begin deletion flow for matching queue/processed records.
- `educator confirm remove {{ concept }}`: confirm deletion started by `remove`.
- `educator alias {{ command_a }} {{ command_b }}`: merge command aliases transitively.
- `educator aliases`: show alias groups.
- `educator aliases remove {{ alias }}`: remove an alias from its current group.

## Data model in `dru_educator`

Rows are pipe-delimited strings in `datum`:

- `alias|queue|add`
- `queue|<unix_timestamp>|<concept>`
- `processed|<unix_timestamp>|<concept>|<summary>`

## Module expectations

- Resolve command aliases transitively before execution.
- `teach` consumes the oldest queue item first.
- `remove` should use explicit confirmation before deleting rows.
- Keep outputs concise and CLI-like unless `teach`/`remind` requires richer prose.
