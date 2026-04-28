# Technical Documentation Sample

## Overview

This document demonstrates how Markdown can be used for technical documentation, combining various elements for clarity.

## System Requirements

| Component | Minimum | Recommended |
|-----------|---------|-------------|
| macOS | 12.0 (Monterey) | 14.0 (Sonoma) |
| RAM | 4 GB | 8 GB |
| Storage | 100 MB | 500 MB |
| Processor | Apple Silicon or Intel | Apple Silicon |

## Installation

### Step 1: Download

Download the latest release from the [releases page](#).

### Step 2: Install

1. Open the downloaded `.dmg` file
2. Drag the application to your **Applications** folder
3. Eject the disk image

### Step 3: First Launch

> **Note:** On first launch, macOS may ask you to confirm you want to open the app since it was downloaded from the internet.

To open the app:
1. Right-click on the application
2. Select "Open" from the context menu
3. Click "Open" in the dialog that appears

## Configuration

The application stores its preferences in:

```
~/Library/Preferences/com.terramar.markdown-reader.plist
```

### Available Settings

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `theme` | String | `"auto"` | Color theme: `"light"`, `"dark"`, or `"auto"` |
| `fontSize` | Integer | `15` | Base font size in points |
| `lineSpacing` | Float | `1.5` | Line height multiplier |
| `showLineNumbers` | Boolean | `false` | Display line numbers in code blocks |

## Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Open File | `⌘O` |
| Close Window | `⌘W` |
| Quit | `⌘Q` |
| Zoom In | `⌘+` |
| Zoom Out | `⌘-` |
| Reset Zoom | `⌘0` |

## Troubleshooting

### App Won't Open

If the application won't open:

1. Check that you're running macOS 12.0 or later
2. Try downloading the app again
3. Reset permissions: `xattr -cr /Applications/Markdown\ Reader.app`

### File Won't Load

Common causes:
- File encoding is not UTF-8
- File is corrupted
- File permissions prevent reading

**Solution:** Try opening the file in a text editor first to verify it's valid.

---

## Support

For bug reports and feature requests, please open an issue on our GitHub repository.

*Last updated: February 2026*
