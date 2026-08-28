# Photo & Video Sorter Pro

A modern, high-performance Python desktop application for automatically organizing large collections of photos and videos by date using a sleek CustomTkinter interface.

This tool scans a source directory using multi-threaded parallel processing, computes MD5 hashes to prevent duplicate imports, extracts photo (EXIF) and video (Hachoir) metadata, and sorts media into a clean **Year → Month → Day** folder hierarchy.

---

## Features

- **Modern Desktop GUI**
  - Built with `CustomTkinter` supporting system-matched dark/light themes.
  - Dedicated configuration windows for granular file-type toggles.

- **High-Speed Parallel Processing**
  - Utilizes Python's `ThreadPoolExecutor` and `scandir` for fast directory traversing and multi-threaded file transfers.

- **Smart Metadata Extraction**
  - **Photos:** Reads EXIF metadata tags (`DateTimeOriginal`, `DateTimeDigitized`, `DateTime`) with support for HEIC/HEIF (iPhone) formats.
  - **Videos:** Extracts native creation timestamps using `Hachoir`.
  - **Fallback:** Uses file modification dates if metadata tags are unreadable.

- **Duplicate Hash Skipping & Auto-Renaming**
  - Computes MD5 file hashes to detect and skip true byte-for-byte duplicates.
  - Automatically appends unique numerical suffixes (`image_1.jpg`) to prevent collisions if different files share identical filenames.

- **Separate Video Destination Support**
  - Option to route videos to a dedicated base directory while photos go to another, keeping video archives organized independently.

- **Dry Run (Simulation) & Operations**
  - Choice between **Move** or **Copy** operations.
  - **Dry Run Mode:** Test and log the proposed directory restructuring without modifying or moving files on disk.

- **Automatic Source Folder Cleanup**
  - Optional post-sort operation to prune empty subdirectories from the source location after files are moved.

- **Date Range Filtering & Progress Tracking**
  - Filter target media within a specific `YYYY-MM-DD` window.
  - Live progress bar, instant UI status logging, and post-run summary window.

- **Robust Error & Crash Handling**
  - Global uncaught exception interceptor logs full stack traces to `~/sort_images_crash_log.txt` and alerts via popup.
  - Handles cross-filesystem and MTP read permission fallback gracefully (`shutil.copy2` + `unlink`).

---

## Folder Structure Output

Sorted media files are organized into the following directory structure:


Destination/
└── 2023/
    └── 7 July 2023/
        └── 7-15-2023/
            ├── IMG_001.jpg
            ├── IMG_002.heic
            └── VID_001.mp4
---

## Requirements
  Python 3.x

Required packages:
  pip install pillow customtkinter hachoir
  Optional (for HEIC support):
    pip install pillow-heif

How to Run
  python main.py

How to Use
  Launch the application
  Select:
    Source Folder (where your media is located)
    Photo Destination Folder (where sorted photos will go)
    Video Destination Folder (optional separate location for videos)
    Log Folder (where logs will be saved)
  Choose:
    File types to include (via File Types menu)
    Date range filter
    Operation mode (Move or Copy files)
    Dry Run mode (simulate without moving files)
    Click Start Sorting
    Monitor progress and live logs in real time
    Use Cancel if needed

How It Works:
  Uses multi-threaded parallel processing for fast directory scanning
  Attempts to read EXIF metadata from photos and Hachoir metadata from videos
  Falls back to file modification timestamp if metadata is missing
  Computes MD5 hashes to detect and skip byte-for-byte duplicate files
  Appends numerical suffixes to prevent filename collisions
  Moves or copies files into structured directories (Year / Month / Day)
  Cleans up empty subdirectories in the source folder if enabled
  Handles file permission and cross-drive issues gracefully (copy + delete fallback)

Notes:
  Files without valid date information fallback to file creation/modification dates
  Duplicate content (matching MD5 hash) is automatically skipped
  Destination files with matching names but different content are safely auto-renamed
  Crashing or unexpected errors are caught globally and logged to a crash file

Future Improvements:
  Thumbnail previews
  Drag-and-drop support
  Exportable summary statistics
  Config file support
  FAISS recognition
  
Author
Henry Belik
July 2025
updated August 2026
