# Notes

Collection of notes, from various fields, in the course of time. </br>
[Obsidian](https://obsidian.md/) software tool, is being used for maintaining this project.

## Search

[`qmd`](https://github.com/tobi/qmd) is a local CLI search engine for markdown vaults. It combines full-text search, semantic search, and LLM re-ranking, so notes can be searched without loading whole files into context. Requires [`bun`](https://bun.sh/).

```bash
bun install -g https://github.com/tobi/qmd
qmd collection add . --name notes
qmd context add qmd://notes "My notes vault"
qmd embed
```

Query it with:

```bash
# Keyword search (BM25).
qmd search "work log okr"

# Semantic search.
qmd vsearch "what did I do on..."

# Hybrid search with LLM re-ranking.
qmd query "how I handle pagination"
```
