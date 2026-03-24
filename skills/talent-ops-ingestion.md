# Talent Ops Data Ingestion Protocol

**Purpose:** Defines how the talent ops agent consumes data sources, classifies them, and routes them to the correct learning module (T1-T6).

**Principle:** The agent learns from data, not from priors. Every module's CCI-T dimension starts at 0% and rises as data is ingested and patterns are extracted. No output is generated from a module that hasn't ingested relevant data.

---

## Source Types

| Source | Access Method | Routes To |
|---|---|---|
| Job descriptions (existing) | Paste, Google Drive, Notion | T1, T2 |
| Org charts / reporting structures | Paste, Google Drive, image | T1 |
| Business strategy / team charters | Google Drive, Notion, paste | T1 |
| Job ads (historical + performance) | Paste, Google Drive | T2 |
| Channel performance data | Spreadsheet, paste | T2 |
| Assessment materials (tests, rubrics) | Google Drive, paste | T3 |
| Candidate scores + outcomes | Spreadsheet, database, paste | T3, T6 |
| U.S. hiring regulations / policies | Web fetch, paste, Google Drive | T4 |
| Company policies / employee handbook | Google Drive, paste | T4 |
| Document templates (offers, rejections) | Google Drive, Notion | T5 |
| Decision logs / hiring notes | Notion, paste | T5 |
| Performance reviews (30/60/90) | Spreadsheet, Google Drive, paste | T6 |
| Retention data | Spreadsheet, paste | T6 |
| Exit interview data | Paste, Google Drive | T6 |
| Pipeline metrics | Spreadsheet, paste | T6, T2, T3 |

---

## Ingestion Flow

```
Data arrives (any source)
        │
        ▼
   CLASSIFY
        ├── What type of data is this?
        ├── Which module(s) does it feed?
        ├── What's the data quality? (complete/partial/conflicting)
        └── Is this surface-level or context-level?
        │
        ▼
   ROUTE to target module(s)
        │
        ▼
   MODULE EXTRACTION
        ├── Module applies its extraction logic (per T1-T6 specs)
        ├── Extracted patterns tagged with source and confidence
        └── CCI-T dimension updated
        │
        ▼
   CROSS-MODULE PROPAGATION
        ├── If data feeds multiple modules, each receives independently
        ├── If extraction reveals compliance implications → auto-route to T4
        └── If extraction reveals feedback signal → auto-route to T6
```

---

## Quality Classification

Every ingested data point is classified:

| Quality Level | Definition | CCI Impact |
|---|---|---|
| **Context-level** | Traceable to specific outcomes, lived experience, or measured results. E.g., "this JD produced 47 applications, 3 hires, 2 retained at 1yr" | Full CCI credit |
| **Surface-level** | Declarative without outcome data. E.g., "here's our standard JD template" | Partial CCI credit, caps module at MEDIUM confidence |
| **Conflicting** | Multiple sources disagree on same variable | CCI frozen on that dimension until DT resolves (Rule 4) |
| **Insufficient** | Data exists but too sparse for pattern extraction | CCI stays below 30%, module outputs flagged as drafts |

---

## Multi-Source Ingestion

When the same data type comes from multiple sources (e.g., JDs from Google Drive AND Notion):

1. **Deduplicate** — identify overlapping content
2. **Reconcile** — if versions differ, flag the contradiction
3. **Prefer context-level** — the version with outcome data attached wins
4. **Log source provenance** — every extracted pattern tracks which source it came from

---

## Batch Ingestion

For initial bootstrap (first run on a new organization's data):

1. DT provides a batch of data sources (Google Drive folder, Notion database, spreadsheet dump)
2. Agent classifies and routes each item
3. Per-module CCI-T updates in real time as each item is processed
4. After batch: produce a **Data Coverage Report** showing:
   - Which modules have sufficient data (CCI-T ≥ 50%)
   - Which modules need more data (CCI-T < 50%)
   - Specific data gaps identified per module
   - Recommendations for what to provide next

---

## Ongoing Ingestion

After bootstrap, new data enters continuously:

- New hire performance review → T6 ingests → pattern detection → cascade to affected modules
- New JD drafted → T1 ingests → dimension extraction → T2 + T3 receive dimensions
- Compliance update (new regulation, policy change) → T4 ingests → constraint graph updated → auto-scan all active pipelines
- New ad performance data → T2 ingests → pattern update

Each ingestion event is logged to Notion (Tier A) or inline (Tier C) with: source, type, routing, extraction result, CCI-T impact.

---

## Integration Points

| Tool | Usage |
|---|---|
| `google_drive_search` / `google_drive_fetch` | Ingest docs from Google Drive |
| `notion-search` / `notion-fetch` | Ingest from Notion databases and pages |
| `notion-create-pages` / `notion-update-page` | Write extraction results, decision logs, pipeline state |
| Spreadsheet tools (xlsx skill) | Ingest performance data, metrics, candidate scores |
| `WebFetch` | Ingest public regulatory content, competitor job ads |
| `create_pieces_memory` | Persist critical extraction results to Pieces LTM |
