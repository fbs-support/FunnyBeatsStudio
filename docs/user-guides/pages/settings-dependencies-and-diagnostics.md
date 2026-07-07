# Settings, Dependencies, and Diagnostics

FunnyBeatsStudio keeps project data, application settings, external tools, and
diagnostics separate. This helps projects stay portable while still allowing
local media and model workflows.

![FFmpeg settings](./images/settings-ffmpeg.png)

## Basic settings

Open `Options > Settings`.

The Basic settings panel includes:

- UI language;
- completion sound for busy operations;
- beat snap range in milliseconds;
- minimum accepted audio beat confidence;
- script export format.

Language changes apply on the next app launch.

The minimum accepted audio beat confidence filters which analyzed markers are
shown and used for snapping. It does not change stored analysis results and is
not the same as High precision detection sensitivity.

## Script export format

The export section chooses the `.funscript` format used by `File > Export
funscript`:

- `1.0`: per-axis sibling files;
- `1.1`: single-file multi-axis with `axes`;
- `2.0`: single-file multi-axis with `channels`.

See [Import, export, and files](./import-export-and-files.md) for the practical
format differences.

## FFmpeg Settings

Open `Options > FFmpeg Settings`.

This panel controls media-tool resolution and media-processing performance:

- explicit `ffmpeg` path;
- explicit `ffprobe` path;
- FFmpeg hardware acceleration;
- optional hardware device;
- decoder, filter, and filter-complex thread counts;
- maximum concurrent FFmpeg processes;
- beatbar frame preparation workers.

Resolution order for `ffmpeg` and `ffprobe` is:

1. explicit user-configured executable path;
2. `tools/ffmpeg/bin` inside the extracted app folder;
3. `PATH`.

Use explicit paths when troubleshooting. Keep `ffmpeg.exe` and `ffprobe.exe`
from the same FFmpeg distribution when possible.

Thread counts of `0` mean FFmpeg default behavior. Increase concurrency and
worker counts carefully; more parallelism can make the machine less responsive
or exhaust GPU/CPU resources.

## Storage Location

Open `Options > Storage Location`.

This panel controls where optional analysis assets and stem separation cache
files are kept. When unset, the app chooses local per-user storage. Custom
locations affect future checks, installs, and stem separation runs.

Changing the asset storage location does not migrate, copy, or delete existing
files. After changing it, check optional Python, stem, and beatbar AI assets
again before using dependent workflows.

Use `Clean Stem Cache` to remove app-created stem cache files in the selected
cache location. The cleanup leaves unrelated files and folders alone.

## Python Runtime

Open `Options > Python Runtime`.

This panel manages the optional Python runtime used by advanced local analysis.
It can:

- check the installed runtime;
- download and extract the required runtime;
- cancel an operation.

The app does not use your global Python installation by default and does not
modify `PATH`.

## Audio Stem Separation Model

Open `Options > Audio Stem Separation Model`.

This panel manages optional High precision audio-analysis assets. It can check
or download the required stem-separation assets after explicit user action.

The panel cannot be used until the Python runtime is current. High precision
beat analysis is enabled only when both the Python runtime and stem assets are
verified.

## Beatbar AI Model

Open `Options > Beatbar AI Model`.

This panel manages optional local AI assets for State (AI) and Cue (AI)
beatbar workflows. It is separate from the audio stem model panel.

The panel can:

- check local asset status;
- download approved assets;
- cancel an operation;
- accept the current local asset notice; and
- save or clear a masked Hugging Face access token for explicit gated downloads.

The token is stored securely and used only for the explicit download action. The
token box is never pre-filled after saving.
There is no CPU fallback for the model-backed beatbar path. Non-AI beatbar
workflows remain available without these AI assets.

## Diagnostics

Open `Options > Diagnostics`.

Diagnostics are local files for troubleshooting. They can include:

- operation logs;
- analysis diagnostics;
- export diagnostics;
- crash reports.

Diagnostics are not project data. Do not paste local diagnostic paths, local
media paths, or machine-specific details into public issue comments, release
notes, or pull request text.

Use the diagnostics panel to open the logs folder or remove app-created
diagnostic files.

## Last-used workflow settings

Some panels remember last-used values in application settings:

- Motion generation stores preview inputs after `Generate preview`.
- Point modifiers store selected-point modifier inputs after a modifier Apply.
- Video replacement export stores export inputs when an export starts.

These settings are restored on the next app launch. They are not saved in
project files and do not include generated previews, temporary export planning
data, diagnostics, or local output paths.

## Settings buttons

Settings panels use:

- `OK`: save and close.
- `Apply`: save and keep the panel open.
- `Cancel`: discard pending edits and close.

Artifact check and download buttons are explicit actions. `Apply` saves pending
settings but does not start downloads or checks.
