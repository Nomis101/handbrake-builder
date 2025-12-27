# handbrake-builder

An configurable, production-grade macOS build script for
building, signing, notarizing and packing HandBrake from source.

This script is intended for advanced users who want
full control over the HandBrake build process while
remaining compatible with Apple’s modern security
requirements.

## Features

- Clean HandBrake source builds
- Automatic dependency management (Homebrew)
- Code signing with Developer ID
- Optional notarization via notarytool
- Structured logging and warning extraction
- Environment preflight validation
- Sensible defaults with overrideable config

## Requirements

- macOS 12 or newer
- Xcode Command Line Tools
- Homebrew
- Apple Developer ID (for signing / notarization)

## Installation

```bash
git clone https://github.com/Nomis101/handbrake-builder.git
cd handbrake-builder
The script can be copied into /usr/local/bin

## Configuration

The script will create a file buildconfig.conf in
$HOME/Library/Application Support/HandBrakeBuilder
that can be used to control the behavior of the script.

Note: AI helped create this script. But I have put everything together,
checked the quality, and tested it several times in different scenarios.
