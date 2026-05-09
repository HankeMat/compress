# Universal Media Compressor

A powerful, interactive shell script wrapper for **FFmpeg** that simplifies the compression and conversion of video and image files. It provides intelligent defaults, size estimations, and processing time forecasts.

## Features

- **Automatic Type Detection:** Automatically detects whether the input is a video or an image.
- **Dual Codec Support:** Choose between **H.265 (HEVC)** for maximum space saving or **H.264 (AVC)** for maximum compatibility with older devices (TVs, legacy players).
- **Smart Presets:** 5 levels of compression (1-5) ranging from archival quality to extreme space-saving.
- **Format Conversion:** Supports multiple containers (MP4, MKV, MOV, AVI) and image formats (WebP, JPG, PNG).
- **Estimation Engine:** Provides estimated output file sizes and processing times before you start, adjusted for the selected codec.
- **Non-Interactive Mode:** Use flags to bypass menus for batch processing or quick use.
- **In-place Replacement:** Optional flag to replace the original file with the compressed version.

## Prerequisites

This script requires **FFmpeg** (including `ffprobe`) and the `file` utility to be installed on your system.

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
compress video.mkv -avi -d -2
```

### Legacy Compatibility (H.264)
If you need the video to play on older hardware (TVs), use the H.264 flag:
```bash
compress video.mp4 -h264 -d -3
```

## Available Flags

| Flag | Description |
| :--- | :--- |
| `-d` | **Delete** the original file after successful compression. |
| `-1`..`-5` | **Strength** level (1 = Best Quality, 5 = Smallest Size). |
| `-h265` | Use **H.265 (HEVC)** codec (Default, best compression, slower). |
| `-h264` | Use **H.264 (AVC)** codec (Higher compatibility, faster, larger files). |
| `-webp`, `-jpg`, `-png` | Force output **Image** format. |
| `-mp4`, `-mkv`, `-mov`, `-avi` | Force output **Video** container. |

## Technical Details

- **Video Compression:** 
    - **H.265:** Most efficient, default for MP4/MKV/MOV.
    - **H.264:** Automatically used for AVI for compatibility.
    - Audio streams are always copied (`copy`) to prevent quality loss.
- **Image Compression:** 
    - **WebP:** Uses `qscale` for high-efficiency lossy compression.
    - **JPG:** Adjusts JPEG quality levels via `q:v`.
    - **PNG:** Optimizes compression levels (lossless).
- **Estimations:** Sizes and times are calculated using `ffprobe` metadata and heuristic multipliers specific to each codec and format.

## Credits

This script is a wrapper around the incredible [FFmpeg](https://ffmpeg.org/) multimedia framework.
