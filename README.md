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

- DEV_DIR=<br>
  Absolute path to your development directory.<br>
  Examples:<br>
  DEV_DIR="$HOME/Developer"<br>
  DEV_DIR="/Volumes/Developer"<br>
  DEV_DIR="$HOME/Documents"<br>

- HB_GIT_REF=<br>
  Git reference to build<br>
  Valid values:<br>
  - master (default)<br>
  - release tags, e.g. 1.10.2<br>
  - latest (highest semantic version tag)<br>
  Examples: HB_GIT_REF="master"<br>
            HB_GIT_REF="1.10.2"<br>

- ENABLE_LOG=<br>
  Log generation, enable (1) or disable (0) collection of compiler log
  into a log file

- ERROR_LOG=<br>
  Error log generation, enable (1) or disable (0) collection of build errors
  into a separate errors log file.

- WARN_LEVEL=<br>
  Compiler warning verbosity (set from 0 to 2).
  Higher levels can generate *many* warnings.

- WARN_LOG=<br>
  Warning log generation, enable (1) or disable (0) collection
  of compiler warnings into a separate warnings log file.

- UPDATE_DEPS=<br>
  Dependency handling (Homebrew).
  Automatically update and upgrade Homebrew dependencies
  before starting the build if set to 1 (disable set to 0).

- AUTO_GIT_PULL=<br>
  Git repository auto-update.
  If set to 1, automatically pull new commits from the HandBrake Git
  repository if the local branch is behind the upstream.

- APPLY_PATCHES=<br>
  Auto apply patches located in the patch folder.

- ADD_CONFIG_OPTS=<br>
  Additional options appended to ./configure.<br>
  Example: ADD_CONFIG_OPTS="--df-jobs=3 --lto=thin"

- NOTARY_ENABLE=<br>
  macOS notarization
  Enable (1) or disable (0) notarization of the built application.

- NOTARY_USERNAME=<br>
  Apple ID used for notarization

- NOTARY_TEAMID=<br>
  Apple Developer Team ID used for notarization

- MAKE_INSTALLER=<br>
  Create an installer file at the end of the build


- Custom compiler flags<br>
Additional compiler flags to append to the build.<br>
These are optional and advanced usage:<br>
CFLAGS=""<br>
CXXFLAGS=""<br>
OBJCFLAGS=""<br>
OBJCXXFLAGS=""<br>

## Folders
The project folder is located at $HOME/Library/Application Support/HandBrakeBuilder<br>
This folder contains subfolders:<br>
git-backups: Backup folder for changes on the sourcode if the branch is changed<br>
logs: Contains build logs, warning logs and error logs (if enabled)<br>
patches: If this folder contains patches (*.patch), this patches will be applied on the sourcecode (if enabled)<br>

## Note
This project includes original code and code generated with the
assistance of OpenAI’s ChatGPT. The author reviewed, integrated, and tested
all components to ensure correctness and reliability.
