# Universal Media Compressor

A powerful, interactive shell script wrapper for **FFmpeg** that simplifies the compression and conversion of video and image files. It provides intelligent defaults, size estimations, and processing time forecasts.

## Features

- **Automatic Type Detection:** Automatically detects whether the input is a video or an image.
- **Smart Presets:** 5 levels of compression (1-5) ranging from archival quality to extreme space-saving.
- **Format Conversion:** Supports multiple containers and formats for both videos and images.
- **Estimation Engine:** Provides estimated output file sizes and processing times before you start.
- **Non-Interactive Mode:** Use flags to bypass menus for batch processing or quick use.
- **In-place Replacement:** Optional flag to replace the original file with the compressed version.

## Prerequisites

This script requires **FFmpeg** (including `ffprobe`) and `file` utility to be installed on your system.

```bash
# Ubuntu/Debian
sudo apt update && sudo apt install ffmpeg
```

## Installation

1. Copy the `compress` script to a directory in your `$PATH` (e.g., `~/.local/bin/`).
2. Make it executable:
   ```bash
   chmod +x ~/.local/bin/compress
   ```

## Usage

### Interactive Mode
Simply provide the path to the file you want to compress:
```bash
compress video.mp4
```

### Direct Mode (Flags)
Bypass the menus by providing the compression level and format flags:
```bash
compress image.png -webp -3
```

### Direct Replacement
To delete the original file and keep only the compressed version:
```bash
compress video.mp4 -d -5
```

## Available Flags

| Flag | Description |
| :--- | :--- |
| `-d` | **Delete** the original file after successful compression. |
| `-1`..`-5` | **Strength** level (1 = Best Quality, 5 = Smallest Size). |
| `-webp`, `-jpg`, `-png` | Force output **Image** format. |
| `-mp4`, `-mkv`, `-mov` | Force output **Video** container. |

## Technical Details

- **Video Compression:** Uses the **H.265 (HEVC)** codec via `libx265`. Audio streams are copied (`copy`) to prevent any loss in sound quality.
- **Image Compression:** 
    - **WebP:** Uses `qscale` for high-efficiency lossy compression.
    - **JPG:** Adjusts JPEG quality levels.
    - **PNG:** Optimizes compression levels (lossless).
- **Time Estimation:** Calculated using `ffprobe` duration and heuristic speed factors based on the selected CRF level.

## Credits

This script is a wrapper around the incredible [FFmpeg](https://ffmpeg.org/) multimedia framework.
