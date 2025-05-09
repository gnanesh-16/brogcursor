<div align="center">

# 🖱️ BrogCursor

<h3>Precise Mouse & Keyboard Action Recorder for Python</h3>

[![PyPI version](https://img.shields.io/pypi/v/brogcursor.svg?style=for-the-badge&logo=pypi&logoColor=white&color=blue)](https://pypi.org/project/brogscursor/)
[![Python versions](https://img.shields.io/pypi/pyversions/brogcursor.svg?style=for-the-badge&logo=python&logoColor=white)](https://pypi.org/project/brogscursor/)


**Record, replay, and automate user interactions with pixel-perfect precision**

[Installation](#installation) • 
[Quick Start](#get-started) • 
[Examples](#examples) • 
[Documentation](#documentation) • 
[License](#license)

</div>

<hr>

<p align="center">
BrogsCursor gives you high-fidelity recording and replay of every mouse movement, click, and keystroke.
Perfect for UI automation, testing, and creating flawless demonstrations.
</p>

```python
from brogscursor import record

recorder = record()
recorder.start_recording()  # Press Esc to stop recording
recorder.replay(recorder.stop_recording())
```

## Table of Contents
- [Installation](#installation)
- [Get Started](#get-started)
- [Features](#features)
- [Creating Your First Recording](#creating-your-first-recording)
- [Using the Command-Line Interface](#using-the-command-line-interface)
- [Customizing Settings](#customizing-settings)
- [Supported Platforms](#supported-platforms)
- [Examples](#examples)
   - [Minimal Example](#minimal-example)
   - [Quick Record Example](#quick-record-example)
   - [Custom Settings Example](#custom-settings-example)
   - [Save to File Example](#save-to-file-example)
   - [Multiple Recordings Example](#multiple-recordings-example)
- [Available Methods](#available-methods)
- [Documentation](#documentation)
- [License](#license)

## Installation

Install the latest stable version from PyPI:

```bash
pip install brogscursor
```

When using this package in your application, it's recommended to pin to at least the major version:

```bash
pip install brogscursor==0.1.*
```

## Get Started

Record and replay user actions in just 4 lines of code:

```python
from brogscursor import record

recorder = record()
recorder.start_recording()  # Press Esc to stop recording
recorder.replay(recorder.stop_recording())
```

## Features

| Feature | Description |
|---------|-------------|
| **Precise Recording** | Capture mouse movements, clicks, scrolls, and keyboard events with high precision |
| **Exact Timing** | Replay actions with the same timing as the original recording |
| **Customizable** | Adjust playback speed, loop count, and more |
| **Control** | Pause/resume recording, stop replay with a hotkey |
| **Resolution Aware** | Automatically scales recorded actions to the current screen resolution |
| **Rich CLI** | Beautiful terminal interface with the Rich library |
| **Multi-format Export** | Save recordings as JSON, CSV, or human-readable text |
| **Robust API** | Comprehensive Python API for integration into your projects |

## Creating Your First Recording

```python
from brogscursor import record
from brogscursor.recorder import BrogsCursorRecorder

def main():
    # Create a recorder instance
    recorder = record()
    
    print("Starting recording - press Esc to stop")
    
    # Start recording (this will block until Escape is pressed)
    recorder.start_recording()
    
    # Save the recording
    recording_file = recorder.stop_recording()
    print(f"Recording saved to: {recording_file}")
    
    # Replay the recording
    print("Replaying recorded actions...")
    recorder.replay(recording_file)

if __name__ == "__main__":
    main()
```

## Using the Command-Line Interface

BrogsCursor provides an interactive CLI for easy recording and playback:

```bash
# Launch the interactive CLI
brogscursor
```

### Keyboard Controls
- `Esc`: Stop recording
- `p`: Pause/resume recording
- `Ctrl+C`: Exit CLI

### CLI Features
- Start recording with optional timeout
- List and manage saved recordings
- Replay recordings with various settings
- Customize configuration

## Customizing Settings

```python
from brogscursor import record

# Create a recorder with custom settings
recorder = record(
    log_dir="my_recordings",   # Custom directory to save recordings
    max_events=10000,          # Maximum number of events to record
    record_keyboard=True,      # Record keyboard events
    speed_multiplier=1.5       # Default replay speed
)

# Start recording with a 30-second timeout
recorder.start_recording(timeout=30)
```

## Supported Platforms

BrogsCursor works across multiple platforms:

- **Windows**: Full support for mouse and keyboard recording/replay
- **macOS**: Full support (requires Accessibility permissions)
- **Linux**: Full support on X11 systems

## Examples

### Minimal Example

```python
import brogscursor

# One-liner recording and replay
brogscursor.record().start_recording().replay(brogscursor.record().stop_recording())
```

### Quick Record Example

```python
from brogscursor import record

# Create recorder
recorder = record()

# Start recording
recorder.start_recording()

# Stop and save recording
recording_file = recorder.stop_recording()

# Replay saved recording
recorder.replay(recording_file)
```

### Custom Settings Example

```python
from brogscursor import record

# Custom recorder configuration
recorder = record(
    log_dir="./custom_recordings",
    max_events=20000,
    record_keyboard=True,
    speed_multiplier=1.5
)

# Start recording with 15-second timeout
recorder.start_recording(timeout=15)

# Replay with custom options
recorder.replay(
    recorder.stop_recording(),
    precision_mode=True,
    loop_count=2
)
```

### Save to File Example

```python
from brogscursor import record
from brogscursor.utils import export_recording
import os

# Record actions
recorder = record()
recorder.start_recording()
recording_path = recorder.stop_recording()

# Export to different formats
exports_dir = "exports"
if not os.path.exists(exports_dir):
    os.makedirs(exports_dir)

# Export as CSV
csv_path = export_recording(recording_path, "csv", os.path.join(exports_dir, "actions.csv"))
print(f"Exported to CSV: {csv_path}")

# Export as human-readable text
txt_path = export_recording(recording_path, "txt", os.path.join(exports_dir, "actions.txt"))
print(f"Exported to text: {txt_path}")
```

### Multiple Recordings Example

```python
from brogscursor import record
from brogscursor.utils import merge_recordings

# Create recorder
recorder = record()

# Record first sequence
print("Recording first sequence - press Esc when done")
recorder.start_recording()
first_recording = recorder.stop_recording()

# Record second sequence
print("Recording second sequence - press Esc when done")
recorder.start_recording()
second_recording = recorder.stop_recording()

# Merge recordings
merged_recording = merge_recordings([first_recording, second_recording], "merged_actions.json")
print(f"Merged recording saved to: {merged_recording}")

# Play merged recording
recorder.replay(merged_recording)
```

## Available Methods

```python
from brogscursor import record
from brogscursor.utils import get_recording_info, export_recording, merge_recordings

# Core recorder methods
recorder = record()
recorder.start_recording(timeout=None)  # Start recording with optional timeout
recorder.stop_recording()               # Stop and save recording
recorder.pause_recording()              # Pause current recording
recorder.resume_recording()             # Resume paused recording
recorder.list_recordings()              # List all saved recordings
recorder.replay(                        # Replay a recording with options
    "recording.json",
    precision_mode=True,
    filter_events=None,
    loop_count=1,
    stop_key='p'
)

# Utility functions
info = get_recording_info("recording.json")  # Get recording metadata
export_recording("recording.json", "csv")    # Export to different format
merge_recordings(["rec1.json", "rec2.json"]) # Combine multiple recordings
```

## Documentation

For complete documentation, see the following resources:

- **Examples**: The `examples/` directory contains fully-commented example scripts.
- **API Documentation**: See the [API Reference](#available-methods) section above.
- **Command-Line Help**: Run `brogscursor --help` for CLI documentation.
- **Source Code**: The source code includes detailed docstrings.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.