# FunnyBeatsStudio Privacy Notice

Version: 2026-07-02

This notice describes how FunnyBeatsStudio handles data in the current local desktop application design.

## Local-first processing

FunnyBeatsStudio is designed to process local media files on your computer. The application does not require a FunnyBeatsStudio account and does not upload your media files, project files, generated `.funscript` files, analysis results, or diagnostic logs to a FunnyBeatsStudio server.

## Network requests

FunnyBeatsStudio may make network requests only when you choose actions that require external resources, such as downloading optional runtimes, packages, or model assets.

Depending on the feature, the app may contact services such as:

- Python.org for the CPython embeddable runtime;
- PyPI or Python package file hosts for Python wheels;
- PyTorch package indexes for CUDA wheels;
- GitHub release assets for some model/config files;
- Hugging Face for DINOv3 model access when you provide a Hugging Face token.

Those third-party services may receive technical information normally sent with web requests, such as IP address, user agent, request time, and requested file URL. Their own privacy policies apply.

## Hugging Face token

DINOv3 model download requires a Hugging Face token with access to the upstream gated model. FunnyBeatsStudio stores the token locally using protected OS storage. Do not include the token in logs, issue reports, screenshots, or shared configuration files.

## Diagnostic logs

If diagnostic logging is enabled, FunnyBeatsStudio may write local logs that can include file paths, media metadata, command-line arguments for external tools, analysis timings, error messages, and local environment details. Diagnostic logs are stored locally and are not uploaded automatically.

Before sharing logs in a public issue, review them and remove sensitive paths, usernames, access tokens, private project details, or media information you do not want to disclose.

## GitHub Issues and public support

If you open a GitHub Issue, the text, attachments, screenshots, logs, or sample files you provide may become public. Do not upload media files you do not have permission to share. Do not post Hugging Face tokens, private paths, private project files, or copyrighted third-party media.

## Telemetry

FunnyBeatsStudio does not include FunnyBeatsStudio-managed analytics or telemetry. If telemetry is added in the future, this notice will be updated before telemetry is enabled, and the app will provide clear controls.

## Contact

For privacy questions, use the support or contact channel published with your copy of FunnyBeatsStudio.
