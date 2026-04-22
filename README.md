Enhanced GUI Photo Sorter
# Enhanced GUI Photo Sorter

A Python-based desktop application for automatically organizing photos and videos by date using a user-friendly graphical interface.

This tool scans a source directory, extracts metadata (EXIF when available), and sorts media into a structured folder hierarchy by **year → month → day**.
---

## Features

- **Automatic file organization**
  - Sorts images and videos into folders by date
  - Structure: `Year / Month / Day`

- **EXIF metadata support**
  - Uses `DateTimeOriginal` when available
  - Falls back to file modification date if needed

- **Graphical User Interface (GUI)**
  - Built with Tkinter
  - Easy folder selection and controls

- **File filtering**
  - Select which file types to include:
    - Images: `.jpg`, `.jpeg`, `.png`, `.heic`
    - Videos: `.mp4`, `.mov`, `.avi`, `.mkv`, `.wmv`, `.mts`

- **Date range filtering**
  - Only process files within a specified date range

- **Progress tracking**
  - Real-time progress bar

- **Logging system**
  - Detailed logs saved to a file
  - Live log output in the GUI

- **Cancel support**
  - Stop sorting safely mid-process

- **Efficient folder handling**
  - Uses caching to avoid redundant folder lookups

---

## Folder Structure Output
Files are organized like this (example):

Destination/
2023/
7 July 2023/
7-15-2023/
image1.jpg
video1.mp4

---

## Requirements
  Python 3.x

Required packages:
  pip install pillow
  Optional (for HEIC support):
    pip install pillow-heif

How to Run
  python your_script_name.py
How to Use
  Launch the application
  Select:
    Source Folder (where your media is located)
    Destination Folder (where sorted files will go)
    Log Folder (where logs will be saved)
  Choose:
    File types to include
    Date range
    Click Start Sorting
    Monitor progress and logs in real time
    Use Cancel if needed

How It Works:
  Attempts to read EXIF metadata from images
  Falls back to file modification timestamp if metadata is missing
  Moves files into structured directories
  Avoids duplicates by skipping existing files
  Handles file permission issues gracefully (copy + delete fallback)

Notes:
  Files without valid date information are skipped
  Duplicate filenames in destination are not overwritten
  Large directories may take time depending on file count

Future Improvements:
  Thumbnail previews
  Drag-and-drop support
  Parallel processing for faster sorting
  Exportable summary statistics
  Config file support
  FAISS recognition

Author
Henry Belik
July 2025
