# MudBlazor #14026 (Fixes #13979): before/after accessibility evidence

Captured 2026-10-14 ~00:26 ET on a local run. Headless Chromium through Playwright 1.62, axe-core 4.14.0.

- **Before:** `ef2caf9` (merge-base of `fix/datagrid-accessible-names` with upstream `dev`)
- **After:** `e25f9c0` (PR head)
- **Test app:** a minimal .NET 10 (SDK 10.0.400) Blazor Server page that references each commit's `src/MudBlazor` project directly. It renders a `MudDataGrid` with `DragDropColumnReordering`, `ColumnsPanelReordering`, `ShowColumnOptions` and `ShowMenuIcon`, and 3 columns. The Columns panel is opened through the settings menu before scanning.

## axe-core violations (whole page)
| rule | before | after |
|---|---|---|
| button-name (critical) | **7 nodes** (6 drag handles + settings-menu button) | **0** |
| label (critical) | 1 (the Columns panel search input, not touched by this PR) | 1 (same) |
| region (moderate) | 8 (test page has no landmarks, an artifact of the test page) | 8 (same) |
| **total rules violated** | **3** | **2** |

## Chromium accessibility tree, `.drag-icon-options` handles
- **Before:** all 6 (3 columns panel + 3 header cells) are `button`, name `""`
- **After:** all 6 are `button`, name `"Reorder column"`

## Files
- `before.png` / `after.png`: real screenshots of the page. A text panel drawn into the page lists, from the captured data, each handle's role and accessible name from Chromium's accessibility tree and the axe violation summary. Handles are outlined red when they have no name and green when they have one. The header-cell handles show only on hover, so only the columns-panel outlines are visible.
- `axe-before.json` / `axe-after.json`: raw axe results
- `a11y-tree-*.json`, `aria-snapshot-*.yaml`: accessible names and the Playwright ARIA snapshot
- `capture-script.js`: the script that produced everything here
