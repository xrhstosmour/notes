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

## Note conventions

- Folders and note files use Title Case, e.g. `Version Control/`, `Naming Conventions.md`.
- Each note's first line is a space-separated list of Obsidian `#tag`s (not YAML frontmatter), e.g. `#ruby #class #classes #object`. Keep this convention, don't switch to frontmatter.
- Cross-reference other notes with `[[WikiLink]]` syntax (the link target is the note's filename without extension), not relative markdown links.
- Fenced code blocks always declare a language, e.g. ` ```ruby `.
- One topic per note file. Prefer adding a new note over growing an existing one into multiple unrelated topics.
- `.obsidian/` is gitignored (local vault config), never commit it.

## Safe-editing rules

- Before renaming or moving a note, `grep -r '\[\[<Note Name>\]\]'` across the repo and update every inbound wikilink, renames silently break links otherwise since Obsidian's own renamer doesn't run in this git-only editing context.
- Don't introduce YAML frontmatter, tags-as-first-line is the existing convention across every note, mixing styles breaks consistency for no benefit.
- `main` is branch-protected, changes go through a feature branch and PR, not a direct push.

## Verification

No build or test suite, this is a notes vault. "Verify" means: wikilinks resolve (no `[[dead links]]` to renamed/removed notes), tags stay consistent with sibling notes in the same folder, and code blocks are syntactically plausible for their declared language.
