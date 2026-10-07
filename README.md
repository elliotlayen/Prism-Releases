<p align="center">
  <img src="assets/icon.png" alt="Prism" width="128" height="128">
</p>

<h1 align="center">Prism</h1>

<p align="center"><strong>Mass-edit Crystal Reports safely.</strong><br>
Change text, formulas, pictures, parameters, fields, SQL commands and sections across ten or a thousand <code>.rpt</code> files in one run — with a full preview first, a backup of every original, and a one-click way back.</p>

<p align="center">
  <a href="../../releases/latest"><strong>Download the latest release →</strong></a>
</p>

---

## Why Prism

Renaming a company, swapping a logo, retargeting a parameter or fixing a formula across a folder of Crystal Reports means opening every report in the Designer and making the same edit again and again. Prism does the edit once, as a rule, and applies it to every report that matches — but only after it has shown you exactly what would change, report by report and line by line, and only to the changes you tick.

Under the hood, Prism edits reports through the Crystal Reports SDK itself, so what it saves is what the Designer would have saved. Text objects are edited at the paragraph level, which means a sentence that mixes typed text with embedded database fields keeps its fields live — the one thing a plain find-and-replace on report text gets wrong.

![Browsing a report in Prism](assets/screenshots/2-preview.png)

## What it does

- **Scan and explore.** Point Prism at a folder (subfolders included) and it indexes every report: sections, text objects, fields, formulas, record selection, parameters, SQL commands, pictures, groups and subreports. Click anything for a syntax-coloured preview. `Ctrl+K` jumps to any report or node by name.
- **Search across reports.** Combine criteria with And/Or, match case, whole words, regular expressions or loose matching (ignores spacing). Results group by report, kind or location, sort by any column, open in a full-size reading view, and export to CSV. Searches can be saved and reopened.
- **Jobs made of rules.** Nine rule kinds, each a small form on a card. Rules validate as you type, duplicate with one click and reorder by drag. Jobs save to a file you can share.
- **Dry run before anything changes.** Every planned change with a Before / After diff, picture changes with the actual image and its placement, warnings where a change needs a look, and a summary per report.
- **Approve what you mean.** Every change has its own tick; a report's tick covers all of its changes. The confirm tells you exactly how many changes in how many reports will be applied.
- **Apply with a safety net.** Every original is backed up before it is touched, every report is journaled as it is edited, and an audit log records what happened. **Restore This Run** puts the originals back byte for byte.
- **Nothing takes the window down.** The Crystal engine runs as a separate process. If it ever fails mid-run, Prism comes back in recovery mode and offers the restore before anything else; outside a run it simply restarts the engine.

![A job with its dry run](assets/screenshots/6-job.png)

## The nine rule kinds

| Rule | What it changes |
|---|---|
| **Text replace** | Text objects (and optionally formulas and SQL commands). Embedded fields are kept intact; a match that would touch one is reported, not applied. |
| **Formula edit** | The text of formula fields, by name match. |
| **Record selection** | The report's record-selection formula. |
| **Image replace** | Pictures, matched by name, section or size, replaced with your file, with a choice of stretch, fit or natural size and a 3×3 anchor. |
| **Parameter edit** | Rename a parameter — every formula, selection and text field that uses it follows — or change its prompt. |
| **Field swap** | Point field objects, text fields, formulas and selection at a different database field. |
| **SQL command** | The SQL of a command object. |
| **Section format** | Suppress, keep-together and page-break flags on sections. |
| **Group field** | The field a group is based on. |

![Picture previews](assets/screenshots/7-image.png)

## Install

**Requirements**

- Windows 10 or 11, 64-bit.
- The **SAP Crystal Reports runtime for .NET Framework, 32-bit, version 13.0.x** (the runtime that ships with Crystal Reports 2013; a machine with the Designer installed already has it).
- .NET Framework 4.7.2 or newer, which is part of Windows 10 and 11.

**Steps**

1. Download `Prism-Setup-<version>.exe` from the [latest release](../../releases/latest).
2. Run it. It installs for the current user only — no administrator rights needed.
3. Windows SmartScreen will warn that the publisher is unknown, because the installer is not code-signed. Choose **More info → Run anyway**. This happens once; updates install silently.

**Updates** are automatic. Prism checks for a new version shortly after it starts and every few hours, downloads it in the background, and shows **Restart to update** in the status bar when it is ready. If you do not restart, the update installs the next time you quit. An update is never installed while changes are being applied. Settings → Updates turns the automatic check off; Help → Check for Updates… works either way, and About → Release notes shows what changed.

## A run, start to finish

1. **Run → Scan Folder…** and choose the folder of reports. Subfolders are included.
2. **File → New Job** (`Ctrl+N`), then **Add Rule** for each edit. Fill in the card; problems are marked on the field they concern.
3. **Dry Run** (`F5`). Read the Changes tab: select a change to see its Before / After, step through with the arrow keys, or expand the pane for a full-size view. Warnings explain anything Prism will not do by itself.
4. Untick anything you do not want. The report row's tick covers the whole report.
5. **Apply Changes.** Confirm the count. Progress shows per report; Cancel stops between reports.
6. The **Logs** tab lists the outcome per report, the backup folder and the audit file. **Restore This Run** undoes it.
7. **File → Save** keeps the job for next time.

![Searching across reports](assets/screenshots/3-search.png)

## Safety, in detail

- Order per report: **backup → open → change → save to a temporary file → close → swap**. A report is never replaced unless its new version saved cleanly.
- Every planned change re-checks the live value against what the dry run saw. If a report changed on disk in between, the change is skipped as *drifted* and reported — never guessed.
- Formulas are validated after editing; an edit that would break a formula blocks the save of that report.
- Backups live in a `.prism-backup` folder beside the reports, one dated folder per run, mirroring the folder structure, with the audit log inside.
- If the engine process dies in the middle of a run, Prism restarts in recovery mode: the interrupted run is listed with the report it was on, and Restore puts every touched report back, that one included.

## Keyboard

| Keys | Action |
|---|---|
| `Ctrl+N` / `Ctrl+F` | New job / new search |
| `Ctrl+O` | Open a job or search |
| `Ctrl+S` / `Ctrl+Shift+S` | Save / Save As |
| `Ctrl+W` | Close the document |
| `F5` | Dry run |
| `Ctrl+K` | Command palette — every command, plus jump to any report or node |
| `Ctrl+B` | Toggle the sidebar |
| `Ctrl+,` | Settings |

![Settings](assets/screenshots/5-settings.png)

## Reporting a problem or asking for something

**Help → Report an Issue…** in the app opens this repository's issue tracker, or go straight to [New issue](../../issues/new/choose). There are templates for a bug report and for an enhancement request. For a bug, include the version from **Help → About Prism** and, if you can, the relevant lines from the log: **Help → Open Logs Folder** opens the folder; `prism.log` records every engine start, run and error.

## Versions

Versions are `YYYY.major.minor`: the year, a number that goes up for major releases, and one that goes up for fixes and small improvements. Every release on the [releases page](../../releases) lists what changed.

---

<p align="center">Created by Elliot Layen</p>
