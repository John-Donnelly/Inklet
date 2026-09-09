# Privacy Policy — Inklet

**Last updated:** 2026-09-09  
**Developer:** JAD Apps (John Donnelly)

## Overview

Inklet is a local text editor for Windows. The developer does not collect,
receive, sell, share or transmit your documents, editor activity or device data.
Inklet does, however, store local application state on your device so settings
and your editing session can survive a restart. This policy describes that local
storage accurately.

## Data sent to the developer

**Inklet sends no personal data to JAD Apps.**

The application has no application telemetry, analytics, advertising, crash
reporting or account service. Your document contents are not uploaded to the
developer.

## Files you open and save

Inklet accesses document files when you explicitly open, create, save, print or
drag/drop them, or when Windows activates Inklet through a registered file
association. Document reads and writes happen locally.

Inklet does not upload document contents to a JAD Apps service or other third
party.

## Local settings and session recovery

Inklet stores preferences such as font, zoom, window state, print settings and
the active-tab index in the Windows application data area
(`ApplicationData.Current.LocalSettings`).

Session recovery uses additional local files. The current implementation writes
`session.json` in Inklet's Windows `ApplicationData.Current.LocalFolder` and can
retain a sibling `session.json.bak` as the previous atomic-write backup. The
session can contain:

- paths of files that were open;
- encoding and line-ending information;
- caret/selection state;
- edit-delta/session state for changed file-backed documents; and
- text needed to restore unsaved/untitled work.

That means unsaved document content can be present on disk inside Inklet's local
application-data folder even though it is never sent over the network. The
session file exists specifically to restore work after restart/crash; users who
handle especially sensitive plaintext should include the Windows user profile
and Inklet application-data folder in their local-device security/cleanup model.

Inklet writes the session atomically through a temporary sibling and may retain a
`.bak` copy of the previous session. These files remain local to the device.

## Network access

Inklet's application code does not intentionally make network requests for
editing, telemetry, analytics, advertising or update checks. There is no
application account or cloud-sync feature.

Windows itself, the Microsoft Store/package infrastructure, SmartScreen or other
operating-system services can have their own network behaviour outside Inklet's
application code and are governed by their respective policies.

## Third-party services

Inklet does not integrate an application analytics/advertising/data-collection
SDK. Its Windows/.NET/WinUI platform dependencies execute locally as part of the
application.

## Children's privacy

Inklet does not operate an online account or developer-side personal-data
collection service. Local files and local session state remain under the Windows
user/device account as described above.

## Changes to this policy

If Inklet's data handling changes, this file and the **Last updated** date should
be updated before the corresponding release is described as having the new
privacy behaviour.

## Contact

Questions about Inklet's privacy behaviour can be raised through the project
repository:

https://github.com/JAD-Apps/Inklet
