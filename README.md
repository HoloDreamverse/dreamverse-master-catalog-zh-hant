# dreamverse-master-catalog-zh-hant

Traditional Chinese text tables of the hololive Dreams master data.

This repository holds only the game's localized text: the `Lang*_Cht`
master tables, decoded to JSONL. It is updated automatically by
[`dreamverse-master-updater`](https://github.com/HoloDreamverse/dreamverse-master-updater)
(`master update --lang-only`).

## Source

The tables come from the JP game server's `Master/Get` response requested with
the header `x-app-lang-type: cht`. For that header the server lists
the same master version as for the Japanese client, plus the `Lang*_Cht`
packs of this language only. The updater downloads just those packs and
decodes their rows with the protobuf schemas of the current game version.

## Layout

```text
master/
├── manifest.redacted.json   # master version, app version, the Lang*_Cht packs (no keys)
├── export-manifest.json     # per-table status and row counts
├── data/Lang*_Cht.jsonl
└── archive/<master-version>/  # tables the server stopped serving
versions/
├── current.json             # current app version / master version
└── <appVersion>.json
diffs/master/                # rows added/removed between master versions
```

Each JSONL row is `{"id": "<text id>", "data": {"id": "<text id>", "text": "<text>"}}`;
an empty text is omitted from `data`.

## Related repositories

Everything that is not text lives elsewhere:

- [`dreamverse-master-catalog`](https://github.com/HoloDreamverse/dreamverse-master-catalog):
  the complete JP master data (all non-text tables, Japanese text), the Octo
  asset catalog, and the in-game notices.
- [`dreamverse-master-catalog-en`](https://github.com/HoloDreamverse/dreamverse-master-catalog-en):
  the same for the EN server, with English text.

Join these tables to the master data by the text id (for example
`la-music_title-m0129` is the title of music `m0129`).
