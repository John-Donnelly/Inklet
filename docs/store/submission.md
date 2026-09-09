# Inklet 2.0.2 — Microsoft Store submission pack

Release-copy pack for the 2.0.2 update. The upload artefact is expected to be:

```text
Inklet (Package)/AppPackages/Inklet (Package)_2.0.2.0_x86_x64_arm64_bundle.msixupload
```

Before reusing this pack for a later version, update the version, screenshots,
measured-performance wording and certification evidence to match that release.

## Package facts

- Version: `2.0.2.0` for this submission pack.
- Architectures: x86, x64, ARM64.
- x86 has an explicit **256 MB per-file limit**. Large-file claims in the Store
  copy refer to the 64-bit builds.
- Large-file performance numbers are measurements from the documented test
  setup/corpus; they are not an unlimited file-size or identical-latency
  guarantee for every PC/storage device.
- Full custom-editor screen-reader/UI Automation accessibility is not yet
  implemented and must not be implied by listing copy.

## Store listing — Description

```text
Inklet is a fast, clean notepad for Windows — everything you want from a plain-text editor, without accounts, ads or application telemetry.

Version 2.0 rebuilds the text engine around memory-mapped source data and a piece-tree editing model so the 64-bit builds can work with very large logs, exports and text datasets without first loading the entire file into one editable string.

BUILT FOR LARGE FILES
• Very large files can show their first viewport while background indexing continues
• The project has benchmarked the 64-bit engine on a 10 GB / ~113-million-line generated corpus; see the published performance notes for hardware/protocol details
• Go To, scrolling and editing use the background/document index instead of a monolithic text buffer
• Find & Replace runs off the UI thread and Replace All is one undo step
• x86 remains limited to 256 MB per file; real limits/latency depend on OS, storage, encoding and available resources

CAREFUL WITH YOUR BYTES
• Atomic save/swap path with tests for byte preservation of untouched data and mixed line endings
• Per-tab undo history and session recovery
• UTF-8, UTF-16 and legacy Windows/code-page support with BOM handling
• Windows CRLF, Unix LF and classic Mac CR detection/preservation paths

EVERYTHING A NOTEPAD SHOULD HAVE
• Multiple tabs with file/cursor/session recovery across restarts
• Word wrap, zoom and light/dark/system styling
• CJK, emoji, proportional-font layout and IME composition support
• Printing with headers, footers and page setup
• Drag and drop plus common text-file associations
• Status bar with line/column, encoding, line-ending and zoom information

PRIVACY
• No account, advertising or application telemetry
• Documents are not uploaded to JAD Apps
• Settings and session recovery are stored locally on the PC; unsaved text can be present in Inklet's local application-data session files so work can be restored after restart

ACCESSIBILITY NOTE
• Standard keyboard editing/navigation is supported; full screen-reader/UI Automation support for the custom editor is still a planned follow-up
```

## Store listing — What's new in this version

```text
Inklet 2.0 introduces a rewritten large-file text engine and a more robust editing/session path.

• 64-bit large-file engine benchmarked on a generated 10 GB / ~113-million-line corpus; first content can appear while indexing completes in the background
• Typing/navigation performance substantially improved versus the old fully-loaded-buffer design; measured figures depend on the hardware and corpus used
• Atomic save/swap path with byte-preservation and mixed-line-ending tests
• Per-tab undo/session state and more efficient recovery of file-backed edits
• Background Find & Replace; Replace All is one undo step
• Improved CJK, emoji, proportional-font hit testing and IME composition
• Fixed failures found in large-file, encoding, selection and session QA

The x86 build remains limited to 256 MB per file. Use x64/ARM64 for large files. Full screen-reader/UIA support for the custom editor is not yet implemented.
```

## Store listing — App features

```text
64-bit engine designed for very large text files
Background indexing for exact line/search metadata
Atomic save/swap with byte-preservation tests
Tabbed editing with local session recovery
Per-tab undo history
Background Find & Replace
UTF-8, UTF-16 and legacy code-page support
Windows, Unix and classic Mac line-ending handling
Word wrap, zoom and light/dark/system styling
Printing with headers, footers and page setup
No account, ads or application telemetry
```

Avoid Store phrases such as **"files of any size"**, **"no file is too large"**,
**"memory stays flat no matter how big the file is"** or **"sub-millisecond at
any file size"**. The project has strong large-file measurements, but Windows,
address-space, x86, filesystem, disk-space, encoding and operation-specific
limits still exist.

## Search terms

```text
notepad
text editor
large files
log viewer
plain text
txt editor
big file editor
```

## Screenshots

Use only screenshots from the exact release build. Existing filenames/captions
can be reused after verifying they still match the UI and measured behaviour:

| File | Suggested caption |
|---|---|
| `01-hero-dark.png` | A fast, clean Windows text editor with tabs, status information and dark mode. |
| `02-gigabyte-file.png` | The 64-bit large-file engine working with a gigabyte-scale generated log while indexing/editing remains available. |
| `03-find-replace.png` | Find & Replace runs in the background so long searches do not block the editor UI. |
| `04-light-theme.png` | Light and dark styling follow Windows; there is no application account or telemetry. |
| `05-menu-open.png` | File, Edit, Format, View and Help commands in Inklet's compact menu. |

## Properties

- Category: Productivity.
- Pricing: Free for the existing listing unless intentionally changed in Partner
  Center.
- System requirement note: x64/ARM64 recommended for large files; x86 refuses
  files above 256 MB.

## Support information

- Website: https://github.com/JAD-Apps/Inklet
- Support: https://github.com/JAD-Apps/Inklet/issues
- Privacy policy: repository `PRIVACY_POLICY.md`

## Certification notes

```text
Update to an existing local text-editor app. No application account is required and Inklet does not upload document contents or send application telemetry.

Inklet edits files selected/opened by the user (picker, drag/drop or registered text-file association). It stores local preferences and session-recovery state in the Windows application-data area; session recovery can include unsaved text so work can be restored after restart.

For large-file testing use the x64/ARM64 build and a generated multi-hundred-MB or larger text/log file. The first viewport can become available while background indexing completes. The x86 build intentionally refuses files above 256 MB.

Full screen-reader/UI Automation support for the custom text editor is not yet implemented; do not use accessibility certification language that implies otherwise.
```

## Pre-submission checklist

- [ ] Run the installed-package QA checklist in `docs/store/qa-checklist.md`.
- [ ] Record current unit/performance/large-file evidence from the exact commit;
      do not copy a historical hard-coded test count.
- [ ] Verify current privacy policy matches the release's local session storage.
- [ ] Verify x86 >256 MB refusal and x64/ARM64 large-file path.
- [ ] Verify screenshots/captions against the release build.
- [ ] Build the StoreUpload bundle and upload the generated `.msixupload`.
- [ ] Paste only the qualified Store copy above.
- [ ] Submit for certification after the release commit/tag and package identity
      have been verified.
