# DeepWiki 2.0.4 Mermaid regression audit

## Test target

- Repository: `maxiaoxuxu/googletest`
- Branch: `test`
- Source baseline: `main @ a8380b01a25ebdb130097b607b3afed2a58d04ba`
- Plugin installed release: `2.0.4`
- Test output: `docs/wiki/_plugin_v2_0_4_retest/`

## Tests performed

1. Read the installed 2.0.4 Mermaid authoring and engine references, plus the packaged `preview.html` and `mermaid-preview.js`.
2. Scanned 15 existing Markdown pages: 11 root Wiki pages, 2 earlier smoke-test pages, and 2 version-2.0.3 retest pages.
3. Extracted 9 Mermaid fenced blocks.
4. Applied the same quoted pipe-edge-label regular expression used by the updated `validate_mermaid.py`.
5. Ran regression fixtures for:
   - `A -->|"Yes"| B` — rejected.
   - `A -->| "No" | B` — rejected.
   - `A -->|Yes| B` — accepted by this static rule.
   - `A -->|No| B` — accepted by this static rule.
   - `A -- "label with punctuation" --> B` — not falsely rejected by this static rule.
6. Re-read the GoogleMock source used by the refreshed page at the pinned source commit and checked the cited line ranges.

## Findings

- The regression detector found 4 bad edge labels in the existing `docs/wiki/08_expectations.md` Mermaid block (source lines 49–52 in that page's fenced block): quoted `no/yes` labels on four edges.
- The other 8 extracted Mermaid blocks had no matching quoted pipe-edge-label pattern.
- The new 2.0.4 test copy `08_expectations.md` uses unquoted pipe labels and updated unique PAGE_ID/AUTOGEN identifiers.
- The original `docs/wiki/08_expectations.md` was not overwritten; the finding is preserved for review.

## Runtime validation status

<escape>not_run</escape> — no `mmdc` executable is installed in the available execution environment, and no browser automation/runtime was available to open the packaged preview page and execute Mermaid.js `parse()` + `render()`. Therefore this audit does **not** claim SVG rendering passed.

The packaged preview uses Mermaid.js 11.4.1 from jsDelivr. Its JavaScript source calls `mermaid.parse()` and `mermaid.render()` for each extracted block, but reading that source is not the same as executing it.

## Result

- Static regression fixtures: passed (5/5 expected outcomes).
- Existing documentation scan: 15 files / 9 diagrams.
- Quoted pipe-edge findings: 4, all in the original `08_expectations.md`.
- New 2.0.4 page copy: corrected.
- Real Mermaid.js or Mermaid CLI parse/render: not run.
- Original Wiki files: unchanged.
