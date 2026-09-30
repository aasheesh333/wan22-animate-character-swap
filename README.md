# wan22-animate-character-swap

Colab notebook for **Wan2.2-Animate character replacement** — replace the person in your video with a character from a reference image, keeping the original motion, expressions, camera movement, lighting and background.

## Open in Colab

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/aasheesh333/wan22-animate-character-swap/blob/main/Wan2.2_Animate_CharacterSwap.ipynb)

Direct link:

```
https://colab.research.google.com/github/aasheesh333/wan22-animate-character-swap/blob/main/Wan2.2_Animate_CharacterSwap.ipynb
```

## What you do
1. Set **Runtime -> Change runtime type -> GPU -> A100 (80 GB)**.
2. **Run all** the cells.
3. When Cell 5 asks, upload **two files**: your driving video and your reference character image.
4. The last cell previews the swapped video and downloads it.

## Requirements
- **A100 80 GB runtime** (Colab Pro+ / RunPod / Lambda). The 14B backbone + encoders need ~45 GB VRAM; the download is ~52 GB.
- Free/Pro Colab (T4 15 GB, L4 22 GB, A100 40 GB) **cannot** run the full pipeline. Use a GGUF + ComfyUI route on those tiers.
- Driving video: MP4/MOV/AVI, one clear main subject, ideally 2–30 s.
- Reference image: 200–4096 px per side, clean front-facing unobstructed shot.

## How it works
The notebook wraps the official [Wan-Video/Wan2.2](https://github.com/Wan-Video/Wan2.2) pipeline in **replacement ("Mix") mode**:
preprocess (`--replace_flag`) produces `src_pose.mp4`, `src_face.mp4`, `src_bg.mp4`, `src_mask.mp4`, then generation runs with `--replace_flag --use_relighting_lora`.

Model weights: [Wan-AI/Wan2.2-Animate-14B](https://huggingface.co/Wan-AI/Wan2.2-Animate-14B) (Apache-2.0).

## Notes
- Replacement mode disables pose retargeting, so match your reference character's body proportions to the on-screen performer.
- The built-in mask extractor is **single-person only**; multi-person clips can track the wrong subject.