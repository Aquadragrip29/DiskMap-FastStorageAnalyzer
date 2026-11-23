<p align="center">
  <img src="https://i.postimg.cc/mrQB8xMX/banner.png" alt="DiskMap Disk Space Analyzer — 3-Second NTFS MFT Storage & Large File Finder for Windows" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-NTFS%20Disk%20Space%20Analyzer-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-diskmap--v1.4-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# DiskMap Disk Space Analyzer — 3-Second NTFS MFT Storage & Large File Finder for Windows

**Drive C: suddenly down to 4 GB free and Windows File Explorer won't show folder sizes? Scan a 1 TB NVMe SSD in 3 seconds via the NTFS Master File Table (MFT), visualize heavy folders, and spot forgotten 50 GB videos, caches, and installers immediately.**

DiskMap Disk Space Analyzer reads the NTFS Master File Table (`$MFT`) directly on Windows instead of slowly crawling folders one by one: **sorting every directory and file by exact size, ranking your Top 100 largest files, and highlighting safe-to-clean caches vs. protected Windows system folders**.

This project is aimed at **Windows 10 and Windows 11 (64-bit) PC users, gamers, and creators** running out of space on `C:` or secondary NVMe/HDD drives.

## Quick Use-Case & Troubleshooting Reference

| Scenario / Issue | Cause | Solution |
| --- | --- | --- |
| Drive `C:` shows 0 GB free, but `Users` folders look small | Hidden `AppData\Local` shader caches, temp installers, and crash dumps | Sort folders by descending size to expose hidden `AppData` bloat in seconds |
| Standard folder scanners take 10+ minutes on a 2 TB drive | Win32 recursive `FindFirstFile` traversal stalls on millions of tiny files | Read the **NTFS Master File Table (`$MFT`)** directly to scan 1M+ files in ~3 seconds |
| Forgotten 40 GB raw OBS recordings or old `.iso` / `.zip` installers | Large single files buried deep inside subfolders | Open the **Top 100 Largest Files** tab to view the biggest files across the entire drive |
| Afraid of accidentally deleting critical Windows or `WinSxS` files | Generic cleaners don't warn before touching protected OS paths | Guard `C:\Windows`, `System32`, and `WinSxS` and move deleted user files to **Recycle Bin** |

## Download for Windows

[**Download DiskMap.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/DiskMap.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why use `DiskMap.exe`? (Key features)

- Scans NTFS drives (`C:`, `D:`, `E:`) in **~3 seconds** using direct Master File Table (`$MFT`) indexing (with fast fallback for exFAT/FAT32 USB drives).
- Displays an interactive **Sorted Folder Tree + Visual Size Treemap** so multi-gigabyte bottlenecks stand out immediately.
- Dedicated **Top 100 Largest Files** and **File Type Breakdown** (`.mp4`, `.pak`, `.zip`, `.iso`, `.vhdx`) views.
- Protects critical Windows OS directories and sends removed user files to the **Windows Recycle Bin** by default.

### Sample Output

```text
[DiskMap] MFT Scan Complete: Local Disk (C:) — 842,190 files indexed in 2.8 seconds
[INFO] [1] C:\Program Files (x86)\Steam   : 184.6 GB (41.2%)
[INFO] [2] C:\Users\Player\AppData\Local  :  76.4 GB (17.1%)  <-- 14.2 GB in Temp & Shader Caches
[INFO] [3] C:\Users\Player\Videos\Captures :  54.8 GB (12.2%)
[OK]   Top Single File  : Raw_Gameplay_4K_60fps.mkv (28.4 GB)
```

The release ZIP is named `DiskMap.zip`; the Windows executable inside is named `DiskMap.exe`.

1. Close DiskMap before updating or replacing executable files.
2. Click **Download DiskMap.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `DiskMap.exe`.
5. Review the options and output paths before processing files.

**Requirements:** Windows 10 or 11 (64-bit); Administrator privileges recommended for instant raw NTFS `$MFT` scanning.

### Verification & Windows SmartScreen Note

- **Offline & standard user permissions:** `DiskMap.exe` runs locally without uploading your personal files and does not require disabling Windows Defender.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project solves

### Instant 3-second scanning on 1 TB–4 TB drives

Reading `$MFT` records sequentially eliminates millions of slow filesystem metadata roundtrips.

### Exposing hidden `AppData\Local` and `ProgramData` bloat

Windows Explorer hides `AppData` by default, even though browsers, Discord, GPU drivers, and launchers store tens of gigabytes there.

### Finding giant forgotten files across the entire drive

The Top 100 Largest Files list immediately surfaces old raw recordings, virtual machine images, and extracted archives.

### Built-in safety rails against deleting system files

Locks critical Windows directories (`Windows`, `WinSxS`, `Boot`) and defaults to Recycle Bin deletion.

## Default folders and configuration paths

DiskMap runs as a standalone portable executable with zero installation or background services:

```text
Portable (Scans NTFS $MFT on C:\, D:\, E:\ directly)
```

Typical directory layout:

```text
DiskMap.exe
├── Folder Tree Tab   : Descending Folder Sizes + Percentage Bars
├── Visual Treemap    : Proportional Interactive Size Blocks
├── Top 100 Files Tab : Single Largest Files Across Entire Drive
└── File Types Tab    : Space Used by .mp4 / .zip / .iso / .pak / .dll
```

Never delete `hiberfil.sys`, `pagefile.sys`, or files inside `C:\Windows\WinSxS` manually—use DiskMap strictly to clean your own user videos, downloads, archives, and temp caches.

## Quick start guide

Follow these steps to get started:

1. **Extract `DiskMap.zip` to a local folder and launch `DiskMap.exe`.** Approve the UAC prompt so DiskMap can read the NTFS `$MFT` at full speed.
2. **Select drive `C:` (or any secondary SSD/HDD) and click **Scan Drive**.** Wait ~2–4 seconds for full drive indexing to complete.
3. **Expand the top folders (`Users\AppData`, `Videos`, `Downloads`) or open **Top 100 Largest Files**.** Identify unneeded recordings, old installers, or duplicate archives.
4. **Right-click unwanted user files and choose **Move to Recycle Bin**.** Empty the Recycle Bin once you confirm everything works properly.

### Data safety note

DiskMap opens storage volumes strictly in read-only scan mode and sends user-selected deletions to the Windows Recycle Bin.

## What the status summary shows

DiskMap displays **total indexed files, scan duration, per-folder GB and % share, Top 100 largest files, and file-extension storage breakdown**.

## FAQ

**Why does DiskMap ask for Administrator permission?**

Windows requires administrator rights to read the raw NTFS Master File Table (`$MFT`) for 3-second full-drive scans; without admin rights, it falls back to standard folder traversal.

**Can DiskMap scan external USB drives formatted as exFAT?**

Yes—it automatically switches to multi-threaded folder scanning on non-NTFS volumes like exFAT SD cards and USB sticks.

**Does DiskMap delete anything automatically?**

No. DiskMap is 100% read-only until you explicitly select a file or folder and move it to the Recycle Bin.

## Useful reading

- [Microsoft Docs — NTFS Master File Table (MFT) Overview](https://learn.microsoft.com/en-us/windows/win32/fileio/master-file-table)

## More Windows Desktop Utilities

- [DupeSweep-HashFileCleaner](../DupeSweep-HashFileCleaner) — Fast SHA-256 duplicate photo, video & download cleaner
- [SteamJunction-LibraryMover](../SteamJunction-LibraryMover) — Move Steam/Epic games between SSDs via NTFS Junctions
- [DX12-ShaderCacheCleaner](../DX12-ShaderCacheCleaner) — GPU Shader Cache & DirectX 12 cleaner for NVIDIA & AMD
- [DriveHealth-NVMeSmartCheck](../DriveHealth-NVMeSmartCheck) — Portable NVMe & SSD SMART health, TBW & temp checker

*Independent open-source desktop utility for Windows.*
