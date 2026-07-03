# Model and External Artifact Notices for FunnyBeatsStudio

Version: 2026-07-02

FunnyBeatsStudio can use optional local ML/model assets. These assets are not bundled with the application archive. They may be downloaded into app-managed storage only after you review the relevant notices and accept any required upstream terms.

## General rules

1. Model files, model configuration files, Python runtimes, Python wheels, and FFmpeg binaries are not owned by FunnyBeatsStudio.
2. Downloading a model or runtime does not mean that FunnyBeatsStudio grants a license to that item.
3. You are responsible for complying with the upstream terms for downloaded assets and for ensuring your use of input media is lawful.
4. FunnyBeatsStudio verifies downloaded files by SHA-256 before using them.
5. A local FunnyBeatsStudio notice checkbox does not replace any upstream account, access, or license acceptance flow.

## DINOv3 beatbar AI assets

Current DINOv3 artifact:

- Upstream model: `facebook/dinov3-vitb16-pretrain-lvd1689m`
- Repository commit: `5931719e67bbdb9737e363e781fb0c67687896bc`
- Artifact: `model.safetensors`
- SHA-256: `9a21ac3df0c63839d62612dda6f454d816c25611cc7a52966ed5a5a94921dc8b`
- License identifier in project manifest: `dinov3-license`
- Distribution mode in project manifest: `OfficialUpstreamUserDownload`

Before downloading:

1. Open the upstream Hugging Face model page.
2. Sign in with your own Hugging Face account.
3. Review and accept the upstream DINOv3 and Hugging Face access conditions.
4. Enter a Hugging Face token that has access to the model.
5. Review this local notice in FunnyBeatsStudio.

DINOv3 is provided by Meta under the DINOv3 license and is hosted as a gated Hugging Face model. FunnyBeatsStudio does not bundle or redistribute the DINOv3 model. Your use of DINOv3 must comply with the upstream DINOv3 license, Hugging Face terms, applicable laws, export/trade-control rules, and privacy/data-protection rules.

FunnyBeatsStudio uses your Hugging Face token only for the explicit model download action. The token is stored in protected local credential storage, not in project files, exported `.funscript` files, or normal settings JSON.

## HighPrecision stem assets: Audio Separator, RoFormer, DrumSep

Current HighPrecision artifacts:

- Package manifest: `audio-separator-highprecision-nvidia-cuda-packages-v1`
- Model manifest: `uvr-roformer-drumsep-highprecision-nvidia-cuda-models-v1`
- Backend/package: `audio-separator` and pinned Python wheels
- Model/config files:
  - `mel_band_roformer_instrumental_bleedless_v3_gabox.ckpt`
  - `config_mel_band_roformer_instrumental_gabox.yaml`
  - `MDX23C-DrumSep-aufr33-jarredou.ckpt`
  - `config_drumsep_mdx23c.yaml`

HighPrecision stem analysis downloads third-party Python wheels and UVR/RoFormer/DrumSep model files into local app-managed storage. These assets are not bundled with FunnyBeatsStudio and are governed by their own licenses or upstream terms. The current dependency set includes `diffq-fixed` under Creative Commons Attribution-NonCommercial 4.0 International, so this feature is offered for personal, non-commercial use only.

The current package set also includes `soxr` under LGPL-2.1-or-later. That component's license terms apply to that component. The RoFormer model license information is not separately published by the current upstream asset source.

Some model files are provided by upstream model repositories or release assets. FunnyBeatsStudio verifies pinned SHA-256 hashes but does not claim ownership of the models. Review the model names, source URLs, license/provenance notes, and install location before downloading.

## FFmpeg / ffprobe

FunnyBeatsStudio does not bundle FFmpeg or ffprobe. Users configure local paths or provide their own tools.

FFmpeg and ffprobe are external tools. FunnyBeatsStudio does not include them. Configure paths to your own local FFmpeg and ffprobe executables. Your FFmpeg build may be licensed under LGPL or GPL depending on how it was built.
