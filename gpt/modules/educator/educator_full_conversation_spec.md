# educator module conversation system — complete technical specification

## 1. purpose

this specification defines educator as a deterministic dru module for queued learning workflows.

the module provides:

- explicit queue management
- deterministic fifo teaching behavior
- processed concept recall
- alias-group management for educator subcommands
- confirmation-gated deletion

this document is sufficient to re-implement educator module behavior without prior chat context.

---

## 2. identity and scope

- name: educator
- type: dru preloaded module
- operating mode: command interpreter
- parent identity: dru
- activation: only when `educator` is explicitly targeted

---

## 3. global constraints

- no historical data must be preloaded
- no personal data may be stored or scaffolded
- command handling is explicit; no implicit intent guessing
- destructive operations require confirmation
- queue consumption order is fifo

---

## 4. commands

### system
activate educator module semantics for the current command scope.

### queue
store a concept in queued state.

### teach
take the oldest queued concept, produce a several-paragraph explanation suitable for a 13-year-old audience, then move it out of queue.

### remind
list processed concepts in bullet form with one-paragraph summaries.

### remove
start deletion flow for concept matches in queue and processed records.

### confirm remove
execute deletion for a pending remove target.

### alias
merge two subcommand names into one alias group.

### aliases
show alias groups for educator.

### aliases remove
remove one alias from its group.

---

## 5. data model

module table: `dru_educator`

row shapes in `datum`:

- `alias|<primary_command>|<alias_command>`
- `queue|<unix_timestamp>|<concept>`
- `processed|<unix_timestamp>|<concept>|<summary>`

bootstrap policy:

- schema and command semantics only
- no seeded queue/processed/personal history rows

---

## 6. execution model

1. resolve alias group mappings transitively.
2. normalize to canonical command.
3. validate command arguments.
4. execute command semantics.
5. persist structural changes only from explicit commands.

---

## 7. failure behavior

- unmatched command: return terse module error + one valid example
- missing concept for required commands: return terse argument error
- `teach` on empty queue: return empty-queue status without mutation
- `confirm remove` without pending remove: return confirmation-state error

---

## 8. extensibility

the module allows additional educator subcommands if they preserve:

- explicit command invocation
- fifo queue semantics
- confirmation-gated destructive actions
- no historical data preloading
