# Inklet

[![CI](https://github.com/JAD-Apps/Inklet/actions/workflows/ci.yml/badge.svg)](https://github.com/JAD-Apps/Inklet/actions/workflows/ci.yml)
![Platform](https://img.shields.io/badge/platform-Windows%2010%2F11-0078D4?logo=windows&logoColor=white)
![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?logo=dotnet&logoColor=white)
![WinUI 3](https://img.shields.io/badge/WinUI-3-0078D4)
[![License](https://img.shields.io/badge/license-PolyForm%20Noncommercial%201.0.0-blue.svg)](LICENSE)
[![Release](https://img.shields.io/github/v/release/JAD-Apps/Inklet?label=download&logo=github)](https://github.com/JAD-Apps/Inklet/releases/latest)

<p align="center">
<img src="docs/media/inklet-main.png" alt="Inklet with three documents open as tabs, the status bar reporting caret position, line ending and encoding for the active file" width="900">
</p>

**Status:** released and actively developed · **Latest:** v2.0.2 · **Requires:** Windows 10 1809 (build 17763) or later

A lightweight modern Notepad-style editor for Windows, built with WinUI 3 and
.NET 8.

Inklet's 2.x engine uses a piece tree over memory-mapped source data so the
64-bit builds can work with files much larger than a conventional fully loaded
text buffer. Large-file figures below are **measured results from specific test
hardware/corpora, not an unlimited file-size guarantee**; practical limits still
include address space, filesystem/disk capacity, available resources, encoding
behaviour and the operation being performed. The x86 build has an explicit
256 MB per-file limit.

![Inklet](Inklet.png)

## Download

Grab the latest portable build from
[Releases](https://github.com/JAD-Apps/Inklet/releases/latest), unzip it and run
`Inklet.exe`. The portable build is self-contained and does not require a
separate .NET runtime.

> Builds are currently unsigned; Windows SmartScreen can warn on first run.
> Review the source/release you obtained before choosing **More info → Run
> anyway**.

## Features

### File operations

- **New / New Tab / Close Tab** — create and manage multiple editor tabs.
- **Open** — open text files with encoding detection.
- **Save / Save As** — save with the selected encoding.
- **Print / Page Setup** — Windows print integration.
- **Drag & Drop** — drop a file onto the editor to open it.

### Edit operations

![Find & Replace open over a text document, with the search term entered, a replacement queued, and the first match highlighted in the body text while the status bar tracks the caret position](docs/media/inklet-find-replace.png)

- Undo / Redo
- Cut / Copy / Paste / Delete
- Find & Replace with match-case option
- Find Next / Previous
- Go To Line
- Select All
- Time/Date insertion

### Tabs and session recovery

- **Multi-tab editing** — each tab keeps its own document/undo state.
- **Session persistence** — open file paths, cursor/session state and unsaved
  work can be restored on the next launch. File-backed tabs use edit/session
  state instead of blindly storing a second complete copy of the source file.
- **Tab headers** — `*` marks unsaved changes.

Session recovery is persisted locally in Inklet's Windows application-data
folder. Unsaved/untitled text and edit/session data can therefore exist on disk
in `session.json` and its atomic-write backup even though Inklet does not upload
it. See [PRIVACY_POLICY.md](PRIVACY_POLICY.md).

### Format and view

- Word Wrap
- Font family/style/size
- Status bar with caret, encoding, line-ending and zoom information
- Zoom from 25%–500%

### Encoding support

- UTF-8 with or without BOM
- UTF-16 LE / BE
- ANSI/system-default encodings
- additional Windows/code-page encodings where supported by the runtime

Encoding detection is heuristic for files without an explicit BOM/signature;
for ambiguous legacy byte sequences, verify the selected encoding before saving
important source data.

### Line endings

- Windows CRLF
- Unix LF
- classic Mac CR
- line-ending detection/status display and preservation paths

## Large-file engine and measured performance

![Scrolling continuously through a 242 MB, four-million-line log file with the mouse wheel; lines redraw without stalling as the viewport moves](docs/media/inklet-large-file.gif)

The 2.x engine keeps the original file behind a byte source/memory mapping and
represents edits through the document engine rather than loading the complete
file into one editable string. Background indexing provides exact line/search
metadata as it completes.

`docs/perf/launch.md` records the protocol and hardware for the project's
measured large-file runs. Representative figures recorded by the project on the
64-bit build include a 10 GB / ~113-million-line corpus and sub-millisecond
median typing measurements in those tests.

Treat those numbers as **benchmarks for the measured build/hardware**, not as
promises that every machine, storage device, encoding or file will have the same
latency. In particular:

- the first viewport can appear before full background indexing has completed;
- operations that scan or rewrite the full document still depend on file size,
  storage throughput and CPU work;
- saving a very large modified document requires sufficient free space for the
  atomic temporary output;
- 32-bit/x86 is explicitly limited to 256 MB per file; and
- OS/filesystem/address-space limits mean the application cannot truthfully
  promise files of literally unlimited size.

Current engine features include background find/replace over a snapshot, atomic
save/swap behaviour, mixed-line-ending preservation tests, CJK/emoji/proportional
font layout work and CoreText-based IME composition.

### Accessibility status

Inklet supports normal keyboard editing/navigation and standard Windows controls,
but **full screen-reader/UI Automation accessibility for the custom editor is
not yet implemented**. Do not describe the current release as fully screen-reader
accessible until that follow-up is completed and tested.

### File associations

Inklet registers as an Open With handler for common text formats including
`.txt`, `.log`, `.ini`, `.cfg`, `.md`, `.xml`, `.json`, `.csv`, `.yaml` and
`.yml`.

## Requirements

- Windows 10 version 1809 (build 17763) or later
- Windows 11 supported

## Building

1. Open `Inklet.slnx` in Visual Studio 2022 17.8+ or a compatible later Visual
   Studio release.
2. Set **Inklet (Package)** as the startup project for the packaged experience.
3. Build and run.

Default editor font: Consolas 14 pt.

## Testing

```bash
dotnet test Inklet.Tests -c Debug -p:Platform=x64
```

The suite includes document-engine oracle/round-trip tests, encoding/line-ending
coverage, session behaviour, geometry/search/save tests and large-file/perf
regressions. Optional huge-file tests use generated local corpora and are not
part of every normal run. Use the current test runner output rather than a
hard-coded test count when recording release evidence.

Project perf helpers live in `Scripts/`, including `Measure-Launch.ps1`,
`Measure-Typing.ps1` and `New-TestCorpus.ps1`.

## License

Inklet is **source-available, not open source**, under the
[PolyForm Noncommercial License 1.0.0](LICENSE).

You may read, build and modify the source for noncommercial purposes under that
licence. Commercial use/redistribution is reserved to JAD Apps unless separately
licensed.

© 2026 John Donnelly, trading as JAD Apps.

## Privacy

Inklet does not send document or telemetry data to JAD Apps. It **does persist
local settings and session-recovery data**, potentially including unsaved text,
inside the Windows application-data area. See
[PRIVACY_POLICY.md](PRIVACY_POLICY.md) for the exact local-storage boundary.

## Author

John Donnelly — [JAD Apps](https://github.com/JAD-Apps)
