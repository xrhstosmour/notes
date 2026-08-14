# AGENTS.md

Personal notes vault, maintained with [Obsidian](https://obsidian.md/) and tracked in git.
This file documents the repository's structure and conventions for agents editing it. For human-facing setup (search tooling), see `README.md`, don't duplicate it here.

## Directory map

| Path | Purpose |
| ---- | ------- |
| `OSes/` | Operating system notes: `Android`, `Linux` (`Arch Linux Based`, `Common`, `Debian Based`), `macOS` (`Apple ID`, `Customization`), `Windows` (several tool/category subfolders, e.g. `Networking`, `Services`, `IIS`) |
| `Programming/` | Programming notes, split by domain: `Cloud`, `Containers`, `Databases`, `ERP`, `Languages`, `Shell`, `Version Control`, `VMs` |
| `Programming/Languages/` | One folder per language (`C#`, `Python`, `Ruby`, ...). A language folder may nest a `Frameworks/<Framework>/` subtree for framework-specific notes |
| `Software/` | Notes about specific applications/tools, one folder per app |
| `Hardware/` | Notes about physical hardware/cabling/device compatibility, not tied to a specific OS or app |

## Note conventions

- Folders and note files use Title Case, e.g. `Version Control/`, `Naming Conventions.md`.
- Each note's first line is a space-separated list of Obsidian `#tag`s (not YAML frontmatter), e.g. `#ruby #class #classes #object`. Keep this convention, don't switch to frontmatter.
- Cross-reference other notes with `[[WikiLink]]` syntax (the link target is the note's filename without extension), not relative markdown links.
- Fenced code blocks always declare a language, e.g. ` ```ruby `.
- One topic per note file. Most existing notes are atomic, a single procedure with numbered steps, not a broad essay, e.g. `Programming/ERP/SBO/Client Services/Restart client services.md`. Match that granularity for a single how-to. Broader reference material (a language's idioms, a tool's full config) can be a longer note, e.g. `Programming/Version Control/Git/Configuration.md`, but still on one coherent topic.
- Nest notes under `<Domain>/<Tool or Category>/<Specific Task>.md`, mirroring existing folders (e.g. `Programming/ERP/SBO/Queries/Price.md`) rather than flattening everything into one file per tool.
- `.obsidian/` is gitignored (local vault config), never commit it.

## Safe-editing rules

- Before renaming or moving a note, `grep -r '\[\[<Note Name>\]\]'` across the repo and update every inbound wikilink, renames silently break links otherwise since Obsidian's own renamer doesn't run in this git-only editing context.
- Don't introduce YAML frontmatter, tags-as-first-line is the existing convention across every note, mixing styles breaks consistency for no benefit.
- Before adding a note that might already exist in some form, search first (`qmd search`/`qmd query`, see `README.md`, or `grep -ri` for the topic), extend or cross-link the existing note instead of creating a near-duplicate.
- `main` is branch-protected, changes go through a feature branch and PR, not a direct push.

## Sensitive data

This vault is git-tracked and may be shared. Before committing any note, especially one migrated from an external source (old personal notes, a work laptop, a screenshot):

- No real credentials: passwords, API keys, tokens, private keys (SSH, WireGuard, TLS), license keys. Replace with a placeholder like `<password>` even in an otherwise-generic example.
- No real hostnames, IP addresses, or internal domain names tied to a specific employer, client, or home network. Replace with placeholders (`<server-ip>`, `SERVERNAME`) or well-known example ranges (`192.168.x.x`, `10.0.0.0/8`).
- No employer, client, or project names. Generalize the underlying technique instead, e.g. "cross-database SQL query permissions" not "how `<client>` queries across their databases."
- No third-party personal data: real names, personal emails/phones, other people's usernames.
- A generic technique with a real-world example attached should keep the technique and drop or placeholder the example's identifying specifics, don't discard genuinely reusable knowledge just because the source material had a real value baked in.
- If a source document (script, config, screenshot) is too entangled with sensitive specifics to safely generalize, leave it out entirely rather than partially redacting it.

## Log

`LOG.md` at the repo root is an append-only, one-line-per-entry record of notable additions to the vault (new domains covered, large imports), newest first. Append to it, don't rewrite past entries.

## Verification

No build or test suite, this is a notes vault. "Verify" means: wikilinks resolve (no `[[dead links]]` to renamed/removed notes), tags stay consistent with sibling notes in the same folder, code blocks are syntactically plausible for their declared language, and no sensitive data as described above.
