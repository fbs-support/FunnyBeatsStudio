# FunnyBeatsStudio

FunnyBeatsStudio is a Windows desktop app for creating and editing multi-axis
`.funscript` timelines from local video files. It helps with beat analysis,
beatbar review, motion draft generation, manual point editing, and export, while
keeping the final timeline under your control.

For the full release-user documentation, start with the
[FunnyBeatsStudio User Guides](docs/user-guides/index.md).

## What you can do

- Load local videos and attach them to editable projects.
- Analyze beats and repair beat timing in the editor.
- Generate motion previews before committing points to the timeline.
- Edit, copy, paste, transform, and review timeline points.
- Import and export `.funscript` files for compatible tools and players.
- Configure optional local analysis assets when you want advanced workflows.

## Before you start

FunnyBeatsStudio release builds are intended for Windows x64 and are distributed
as portable release ZIP files. Extract the ZIP before running the app.

FFmpeg and ffprobe are required for media workflows. FunnyBeatsStudio does not
bundle them, so configure their paths from `Options > FFmpeg Settings`, place
them under `tools/ffmpeg/bin` next to the app, or make them available on `PATH`.

Optional Python and AI model assets are managed from the app settings panels and
are only needed for advanced analysis modes.

## Quick start

1. Extract the release ZIP to a normal user-writable folder.
2. Run `FunnyBeatsStudio.App.exe`.
3. Open `Options > FFmpeg Settings` and confirm `ffmpeg` and `ffprobe`.
4. Load a video with `File > Load video`.
5. Save a `.fbsproj` project file.
6. Run beat analysis, generate a motion preview, and apply the result if useful.
7. Review and edit the timeline manually.
8. Export `.funscript` files from `File > Export funscript`.

See the [Quick start guide](docs/user-guides/pages/quick-start.md) for the
step-by-step version with screenshots.

## Documentation

- [Installation and requirements](docs/user-guides/pages/installation-and-requirements.md)
- [Quick start](docs/user-guides/pages/quick-start.md)
- [Editor basics](docs/user-guides/pages/editor-basics.md)
- [Beat analysis and editing](docs/user-guides/pages/beat-analysis-and-editing.md)
- [Motion generation](docs/user-guides/pages/motion-generation.md)
- [Import, export, and files](docs/user-guides/pages/import-export-and-files.md)
- [Troubleshooting](docs/user-guides/pages/troubleshooting.md)

## Notes

Generated timelines are drafts. Always review timing, point placement, speed
limits, and export format before using the result elsewhere.

Project files store editor state and references to your media. They do not embed
the original video, FFmpeg binaries, local model files, or generated exports.

## Legal and privacy

- [License](LICENSE.md)
- [Privacy](PRIVACY.md)
- [Third-party notices](THIRD_PARTY_NOTICES.md)
- [Model and external artifact notices](MODEL_AND_EXTERNAL_ARTIFACT_NOTICES.md)

## Support

If this tool helps your workflow, you can leave a small tip or support development here:

[<img src="https://storage.ko-fi.com/cdn/kofi1.png?v=6" width="128px" alt="Buy me a coffee">](https://ko-fi.com/T3S522HQE2)

Support goes toward hosting, testing, documentation, and ongoing maintenance.

## Changelog

### 1.0.0

Initial release build.
