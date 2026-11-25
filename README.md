# FileOrganizeEngine

**FileOrganizeEngine** is a Windows PowerShell project for organizing files in a selected folder by extension or by a predefined smart category. The Smart File Organizer V3.2 source also contains safeguards and recovery-oriented routines intended to help protect files during organization.

> [!IMPORTANT]
> **The checked-in PowerShell source is currently incomplete and cannot be treated as a runnable release.** Its main workflow stops during journal initialization: the `try` block is not completed, the `throw` statement uses an invalid `-ForegroundColor` parameter, and the organization/move-and-journal execution code is absent from the end of the file. Do not run it against important files until the source has been completed and tested. See [the review notes](docs/REVIEW.md).

## Features present in the source

The existing `PowerShell Code` file includes implementations or definitions for:

- **Two organization modes:** sort by lowercase file extension or by smart category.
- **Smart categories:** Images, Videos, Audio, Documents, Archives, Installers, Code, Shortcuts, and Others.
- **Folder selection:** a Windows Forms folder browser dialog.
- **Safety checks:** reject protected locations and paths containing reparse points; skip hidden, system, and reparse-point files.
- **Preflight and preview:** build a proposed move plan, reject unsafe/conflicting destinations, and calculate SHA-256 fingerprints before confirmation.
- **Recovery-oriented journal routines:** JSON journal writing, prior-journal backup with hash verification, and undo logic that checks recorded paths and hashes before restoring.

Because the main execution workflow is incomplete, these source-level routines must not be interpreted as proof that end-to-end organization, journaling, or undo currently works.

## Requirements

- Windows (the script uses `System.Windows.Forms` and Windows-specific folder protections).
- Windows PowerShell or PowerShell on Windows with the Windows Forms assembly available.
- Permission to read and move files in the chosen folder.

No dependency manifest, automated test suite, or launcher is currently present in the repository.

## Intended usage

The intended interactive flow in the source is:

1. Start the organizer and choose **Organize files** or **Undo last session**.
2. Select a folder to work with.
3. For organization, select **By extension** or **By smart category**.
4. Review the proposed file moves and confirm or cancel.
5. For recovery, choose **Undo last session** and review the result.

The source file is currently named `PowerShell Code` (without a `.ps1` extension). Once the source is repaired and tested, the intended launch command from the repository root is:

```powershell
powershell.exe -NoProfile -ExecutionPolicy Bypass -File ".\PowerShell Code"
```

**This command is not expected to work with the current incomplete source.** The execution policy option is shown only as a launch example; follow your organization's PowerShell policy and review scripts before running them.

## Safety guidance

- Test only with disposable copies of files until the missing execution workflow has been restored and validated.
- Keep independent backups. A recovery journal is not a substitute for a backup.
- Review the preview carefully before confirming any future organization run.
- Do not use the organizer on system folders, protected data, or folders containing valuable files until tests cover moves, collisions, interruption, journal recovery, and undo.

## Repository contents

```text
.
├── LICENSE          MIT license
├── PowerShell Code  Smart File Organizer V3.2 PowerShell source (incomplete)
├── README.md        Project overview and usage guidance
└── docs/
    └── REVIEW.md    Source review findings and repair checklist
```

## License

This project is distributed under the MIT License. See [LICENSE](LICENSE).
