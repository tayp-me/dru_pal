# dru Module Export: educator

Canonical export of the **educator** module for dru.

Includes: - dru registry upserts - module table schema - alias/queue/processed
row formats (scaffold only; no seeded module data)

------------------------------------------------------------------------

## SQL Export

``` sql
-- dru module export: educator
-- canonical schema + inserts
-- generated: 2026-02-22 (America/Denver)

BEGIN;

-- registry table
CREATE TABLE IF NOT EXISTS dru (
  id SERIAL PRIMARY KEY,
  name_machine VARCHAR(25) NOT NULL,
  command_machine VARCHAR(25) NOT NULL,
  command_semantic TEXT NOT NULL
);

-- module table
CREATE TABLE IF NOT EXISTS dru_educator (
  id SERIAL PRIMARY KEY,
  datum TEXT NOT NULL
);

-- registry rows (upsert)
CREATE UNIQUE INDEX IF NOT EXISTS dru_name_command_uq ON dru (name_machine, command_machine);

INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','queue','store a concept that I want to learn more about')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;
INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','remind','list out all processed queue concepts with a bulletpoint and a one paragraph summary of the concept')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;
INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','teach','take the oldest item from the queued concepts and explain it to me like I am 13 in several paragraphs, and then remove it from the queue')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;
INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','remove','removes both queued and processed rows of {{ concept }} with a confirmation dialog, to make sure it''s a correct match')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;
INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','alias','merge two subcommand names into one alias-group; order-independent; resolves aliases transitively and merges behaviors')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;
INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','aliases','show alias groups for the module')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;
INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','aliases_remove','remove an alias name from its group (command shape: {{ mod }} aliases remove {{ alias }})')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;
INSERT INTO dru (name_machine, command_machine, command_semantic)
VALUES ('educator','confirm_remove','confirmation step for remove (command shape: {{ mod }} confirm remove {{ concept }})')
ON CONFLICT (name_machine, command_machine) DO UPDATE SET command_semantic = EXCLUDED.command_semantic;

-- module data rows
-- scaffold-only export: no data preloaded into dru_educator

COMMIT;
```
