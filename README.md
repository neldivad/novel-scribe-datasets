# novel-scribe-datasets

Open datasets for **dialogue-driven narrative analysis** — characters, threads, reveals, and the slow
drift of who people become. Everything here is plain Markdown in a small, consistent shape — the **NVS**
convention (*Novel Visual Studio*, described below) — so it loads into
[novel-scribe](#using-with-novel-scribe) or any tool that reads speaker-tagged dialogue.

There are two kinds of dataset here:

| Dataset | What it is | Size |
|---|---|---|
| [`office-drama/`](office-drama) | A hand-authored workplace layoff comedy where the AI assistants (Opus, GPT-6.7, Grok-4.2) are characters with hidden agendas. Ships with an **answer key** so extraction, coherence, and revelation can be *scored*, not just demoed. | 24 scenes, 4 chapters |
| [`shakespeare/`](shakespeare) | Ten full public-domain Shakespeare plays — acts as chapters, scenes as files, multi-character and coherent, dense with the dramatic irony, mistaken identity, and revelation that narrative tools exist to find. | ~191 scenes, 10 plays |

> **Spoiler note:** `office-drama/OUTLINE.md` and `office-drama/ground-truth.md` are the design doc and the
> answer key — they reveal every twist on purpose. Read the scenes first if you'd rather be surprised.

## The format (NVS)

**NVS** (Novel Visual Studio) is just disciplined Markdown — no proprietary markup. Each dataset is a
self-contained project:

```
<project>/content/
  story/chapters/<NN>-<chapter>/<NN>-<scene>.md   # scenes, read in order
  world/characters/<name>.md                      # a wiki page per character
```

- A **scene** is YAML frontmatter (`scene_id`, `title`, `chapter`, `characters_present`) followed by
  `## Scene` and dialogue lines of the form `**Speaker:** their line`. That's it — no proprietary markup.
- A **character** page is frontmatter (`id`, `name`, …) plus free-text sections.

Because it's just Markdown, you can read, diff, and edit any of it by hand.

## Provenance

- **office-drama** is original, hand-authored work (design in `office-drama/OUTLINE.md`).
- **shakespeare/** was generated from Project Gutenberg editions by the `shakespeare` web source in the
  companion **game-story-extractor** project and committed here because the text is public domain. It is
  fully regenerable.

## Scale & copyrighted corpora (intentionally not here)

Larger or copyrighted sources — Game of Thrones, The Office, and the like — are **not** committed to this
repo. They live as *web sources* in **game-story-extractor**, which downloads and transforms them into this
same NVS shape on your own machine; the output stays local. This repo only carries content that is free to
redistribute.

## Using with novel-scribe

```bash
scribe ingest-nvs --path office-drama        --work-id office
scribe ingest-nvs --path shakespeare/hamlet  --work-id shakespeare-hamlet
# every play: see shakespeare/PROJECTS.md
```

## License

Original content is released under **CC0 1.0** (public-domain dedication) — use it freely, no attribution
required. `shakespeare/` is itself public domain via Project Gutenberg. See [`LICENSE`](LICENSE) for the
full notice and source attribution.
