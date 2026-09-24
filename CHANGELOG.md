# Changelog

All notable changes to `qalainau/filament-warp-table` will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- `->warp()` for Filament 5 tables: the records area is drawn on a `<canvas>` while the header, toolbar,
  filters, pagination, bulk actions and modals stay Filament's own.
- Canvas rendering for `TextColumn`, `IconColumn`, `ImageColumn`, `ColorColumn`, `TextInputColumn`,
  `SelectColumn`, `ToggleColumn` and `CheckboxColumn`; other columns are rendered as DOM overlays for
  the rows on screen.
- Inline editing through Filament's `updateTableColumnState`, with validation errors.
- Grouping: collapsible groups, HTML group titles, descriptions and group selection.
- Summaries: group subtotals, page summary and table summary. Summary rows hidden by application CSS
  are hidden in the canvas too.
- Multi-level rows (`->warpMultiLevel()`): each record spans several lines on a grid, with a
  multi-level header (`HeaderCell`). Columns are placed with `->warpCell()`.

### Fixed

- Closer match with the native table, found with side-by-side demos:
  - Action colors default to `primary` (`gray` in dropdowns), button and badge actions use the `sm` size,
    and rows with button actions are as tall as in the native table.
  - The first and last cells get the native edge padding (`ps-6` / `pe-6` for action cells), and the
    actions header follows the actions alignment.
  - Text inputs draw `prefix()` / `suffix()` as separate sections, and disabled or saving inputs use the
    native disabled colors. Long values are clipped like an `<input>`.
  - Badges use the native letter spacing, limited lists show the translated "and N more", bulleted lists
    use the native marker indent, and icons are separated from the text by a space and sized by the text size.
  - Wrapped text and headers no longer break early because of sub-pixel differences or trailing spaces,
    and line clamping puts the ellipsis at the end of the last line.
  - Image columns use the native default sizes (2.5rem, 2rem when stacked, natural aspect ratio when
    neither circular nor square).
  - HTML, Markdown and custom view columns are rendered with the native cell markup, and all of them are
    measured with that markup, so column widths match the native table.
  - Column widths also consider the widest rows beyond the measurement sample.
- `->recordClasses()`: background colors assigned to the classes by application CSS are drawn.
- Native-table behavior parity:
  - Page scrolling by default; `->warpHeight()` for a fixed-height scroll area with a sticky header.
  - Row and URL-action links are real links (new tab with Cmd/Ctrl-click, middle-click, context menu).
  - Shift-click range selection.
  - Keyboard focus in the native Tab order with native-looking focus rings; Enter / Space activation.
  - Loading states (disabled checkboxes, sort spinner) while Livewire is busy.
  - Column widths measured by the browser from a hidden table with Filament's markup.
  - Browser find (Cmd/Ctrl+F) across all rows, including rows that are off screen.
- Automatic fallback to the native table for column layouts, reorder mode, groups-only tables and
  empty results.
- Asset URLs include a hash of the file contents, so browsers never keep a stale build.
