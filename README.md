# handbrake-builder

An configurable, production-grade macOS build script for
building, signing, notarizing and packing HandBrake from source.

This script is intended for advanced users who want
full control over the HandBrake build process while
remaining compatible with Apple’s modern security
requirements.

## Features

- Automated end-to-end build of HandBrake from upstream GitHub sources
- Repository cloning, updating, and clean rebuilds
- Automatic dependency installation and validation via Homebrew
- Environment preflight checks (Xcode, Command Line Tools, SDKs, codesigning identities)
- Deterministic build configuration with sensible defaults and overrideable settings
- Structured logging of all build phases (configure, compile, link, package)
- Robust extraction of primary compiler and build-system warnings / errors
- Generation of a concise, human-readable warning / error log suitable for CI and local development
- macOS code signing using Developer ID Application
- Optional notarization via notarytool, including submission and status handling
- Safe handling of interrupted or failed builds
- CI-friendly, non-interactive operation
- Fully compatible with macOS default tooling (BSD awk, zsh)
- Designed for easy integration into existing shell-based build pipelines

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
```

## Configuration

The script will create a file buildconfig.conf in
$HOME/Library/Application Support/HandBrakeBuilder
that can be used to control the behavior of the script.
In the same folder logs and backup files will be stored (if enabled).

Note: This project includes original code and code generated with the
assistance of OpenAI’s ChatGPT. The author reviewed, integrated, and tested
all components to ensure correctness and reliability.
