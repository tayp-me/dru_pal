# Addendum: Module Table Export to Downloadable SQL (No Flags)

**Feature Name:** Module SQL Export  
**Purpose:** Export a module’s persistent data table (`dru_<name_machine>`) into a portable `.sql` file (schema + inserts) that can be downloaded and imported elsewhere.

---

## `mod export {{ name_machine }}`

Exports a module’s dedicated table (`dru_{{ name_machine }}`) as a SQL script and returns a downloadable `.sql` file.

### Behavior
When the user runs:

`mod export {{ name_machine }}`

Dru will:

1. Validate that `{{ name_machine }}` exists in the registry (`dru` table).
2. Read all rows from `dru_{{ name_machine }}`.
3. Generate a SQL script containing:
   - `CREATE TABLE dru_{{ name_machine }} (...)`
   - `INSERT INTO dru_{{ name_machine }} (id, datum) VALUES ...;` for each row
4. Provide the resulting file as a downloadable artifact named `dru_{{ name_machine }}.sql`.

### SQL Script Format (Default)
Default is **PostgreSQL-like SQL**, using:

- `id SERIAL PRIMARY KEY`
- `datum TEXT`

Example schema:

`CREATE TABLE IF NOT EXISTS dru_example ( id SERIAL PRIMARY KEY, datum TEXT );`

### Data Escaping Rules
To preserve round-trippability:
- Single quotes in `datum` are escaped as `''`.
- Newlines in `datum` are preserved consistently (either literal newlines within the SQL string or escaped as `\n`, but the export must use one approach consistently within the file).

---

## Failure Modes
- If the module does not exist: return a terse CLI error (no file generated).
  - Example: `ERROR: module 'journal' not found`
- If the module exists but has no rows:
  - Still generate a valid `.sql` containing the `CREATE TABLE` statement (no inserts).

---

## Example Session

- `mod new journal`
- `journal subcommand add "Insert '{{ argument }}' into dru_journal"`
- `journal add First note`
- `journal add Second note`
- `mod export journal`

Result: downloadable `dru_journal.sql` including table definition and inserts.
