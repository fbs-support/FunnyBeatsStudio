# Third-Party Notices for FunnyBeatsStudio

Version: 2026-07-02

This document summarizes third-party software used by or with FunnyBeatsStudio. It is not a substitute for the full license texts supplied by each third-party project.

## Scope

FunnyBeatsStudio is proprietary freeware. Third-party components are licensed by their respective owners under their own terms.

This document covers:

1. components included with or required by the FunnyBeatsStudio desktop application;
2. optional app-managed downloads triggered by the user;
3. external tools configured by local path and not bundled with the application.

Model-specific notices are in `MODEL_AND_EXTERNAL_ARTIFACT_NOTICES.md`.

## Components included with or required by the app

| Component | Version | Purpose | License / notice |
|---|---:|---|---|
| Microsoft Windows App SDK Runtime | 2.2.0 | WinUI / Windows desktop app runtime support | Microsoft package license terms |
| Microsoft Windows App SDK WinUI | 2.2.1 | WinUI UI framework components | Microsoft package license terms |
| Microsoft.Graphics.Win2D | 1.4.0 | 2D graphics rendering | Microsoft package license terms |
| OpenCvSharp4 | 4.13.0.20260602 | .NET OpenCV wrapper | Apache-2.0 according to NuGet metadata |
| OpenCvSharp4.runtime.win.slim | 4.13.0.20260602 | Native OpenCV runtime for Windows slim package | Apache-2.0 according to NuGet metadata; this slim package is selected to avoid bundling FFmpeg |
| .NET runtime files | Varies by app version | .NET runtime support | Microsoft .NET license terms |

## External tools not bundled

### FFmpeg / ffprobe

FunnyBeatsStudio does not bundle FFmpeg or ffprobe. Users may configure local executable paths, rely on `PATH`, or place user-provided tools in a supported local tools directory.

FFmpeg builds can be LGPL or GPL depending on build configuration and enabled libraries. Your rights and obligations for FFmpeg or ffprobe come from the build you choose to use, not from FunnyBeatsStudio.

## Optional app-managed downloads

FunnyBeatsStudio may download third-party runtimes, wheels, and models into local app-managed storage when the user explicitly chooses that feature. These files are not part of the application source license and may have separate terms.

| Asset group | Current source pattern | Notice |
|---|---|---|
| CPython embeddable runtime | `https://www.python.org/ftp/python/...` | Python Software Foundation License Version 2. Python's `LICENSE.txt` is installed with the runtime. |
| DINOv3 package wheels | PyPI / PyTorch CUDA wheel indexes | Governed by each wheel's license. See `THIRD_PARTY_PYTHON_WHEELS.md`. |
| HighPrecision Audio Separator package wheels | PyPI / PyTorch CUDA wheel indexes | Governed by each wheel's license. See `THIRD_PARTY_PYTHON_WHEELS.md`. |
| DINOv3 model file | Hugging Face gated model repository | Requires the user's own Hugging Face account/access and DINOv3 license acceptance. See `MODEL_AND_EXTERNAL_ARTIFACT_NOTICES.md`. |
| RoFormer / DrumSep model and config files | `nomadkaraoke/python-audio-separator` model-config release assets | Model provenance and license notices are shown before download. See `MODEL_AND_EXTERNAL_ARTIFACT_NOTICES.md`. |

## License-sensitive optional dependencies

The current HighPrecision package manifest includes at least these license-sensitive dependencies:

| Package | License in current manifest | Notice |
|---|---|---|
| `diffq-fixed` | Creative Commons Attribution-NonCommercial 4.0 International | The current HighPrecision feature is offered for personal, non-commercial use only while this dependency remains in the package set. |
| `soxr` | LGPL-2.1-or-later | The LGPL terms for this component apply. FunnyBeatsStudio's license does not remove rights granted by that component license. |

## Attribution and source links

FunnyBeatsStudio includes these user-facing notice files:

- `LICENSE.md`
- `THIRD_PARTY_NOTICES.md`
- `THIRD_PARTY_PYTHON_WHEELS.md`
- `MODEL_AND_EXTERNAL_ARTIFACT_NOTICES.md`
- `PRIVACY.md`
