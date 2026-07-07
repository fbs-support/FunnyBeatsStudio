# Installation and Requirements

FunnyBeatsStudio is a Windows desktop app for creating editable multi-axis
`.funscript` timelines from PMV. The app is designed for AI-assisted editing:
it helps analyze beats, beatbars, and motion drafts, but you should review
and adjust the result before export.

![FFmpeg Settings](./images/settings-ffmpeg.png)

## Supported environment

- Windows x64.
- A release ZIP built for `win-x64`.
- Local video files that FFmpeg can read.
- Enough disk space for extracted app files, project files, diagnostics, and
  optional local analysis assets.

The release ZIP is self-contained for the .NET desktop app runtime. End users do
not need to install the .NET SDK to run the release build.

## Required external tools

FunnyBeatsStudio does not bundle FFmpeg or ffprobe. Install or provide both
tools before using media workflows such as video loading, audio analysis,
beatbar analysis, or video replacement export.

You can make FFmpeg available in one of these ways:

- Set explicit paths in `Options > FFmpeg Settings`.
- Place the tools in `tools/ffmpeg/bin` inside the extracted app folder.
- Add `ffmpeg` and `ffprobe` to `PATH`.

Use matching builds of `ffmpeg.exe` and `ffprobe.exe` from the same FFmpeg
distribution when possible.

## Optional dependencies

Some advanced analysis modes use optional local assets:

- `Options > Python Runtime` manages the optional Python runtime for advanced
  analysis.
- `Options > Audio Stem Separation Model` manages optional High precision
  audio-analysis assets.
- `Options > Beatbar AI Model` manages optional local beatbar AI assets.

The app does not use your global Python installation by default. Optional assets
are checked, installed, and verified through the settings panels, after explicit
user action.

High precision audio analysis and model-backed beatbar AI features may require a
compatible NVIDIA GPU, matching driver support, and enough VRAM. Simpler
editing, import/export, manual beat editing, and non-AI beatbar workflows remain
available without those optional assets.

## Install from a release ZIP

1. Download the release ZIP and matching `.sha256` file, if provided.
2. Extract the ZIP to a normal user-writable folder.
3. Run `FunnyBeatsStudio.App.exe` from the extracted folder.
4. Open `Options > FFmpeg Settings`.
5. Confirm that `ffmpeg` and `ffprobe` resolve correctly, or set their explicit
   paths.
6. Load a video with `File > Load video`.

Do not run the app directly from inside the compressed ZIP. Extract it first so
the app and its supporting files can be found normally.

## First-run checklist

- Open `Options > Settings` and choose your preferred language if needed.
- Open `Options > FFmpeg Settings` and confirm media tool paths.
- Leave FFmpeg hardware acceleration on `Disabled` or `Auto` until basic
  loading and playback work.
- Open `Options > Diagnostics` only when you need extra logs for troubleshooting.
- Install optional Python, stem, or beatbar AI assets only if you plan to use
  High precision or model-backed analysis.

## Updating the app

1. Close FunnyBeatsStudio.
2. Extract the new release ZIP to a new folder, or replace the old extracted app
   folder.
3. Start `FunnyBeatsStudio.App.exe`.
4. Recheck `Options > FFmpeg Settings` if media tools stop resolving.

Project files and application settings are separate from the release ZIP. Keep
your `.fbsproj`, `.funscript`, source videos, and exported files outside the app
installation folder.

## Uninstalling

FunnyBeatsStudio release ZIP builds are portable. To remove the app, close it
and delete the extracted app folder.

Application settings, diagnostics, caches, and optional analysis assets may
live outside the extracted app folder. Use the settings panels to review storage
locations before deleting external data manually.
