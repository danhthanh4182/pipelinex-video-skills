---
name: generate-comfyui-video-assets
description: Build reproducible ComfyUI workflows for illustrations, B-roll candidates, image sequences and reference-conditioned video assets. Use for local graph design, model setup, GPU constraints and PipelineX visual handoff.
---

# Generate ComfyUI Video Assets

1. Specify the subject, use in the edit, aspect ratio, duration if animated, output size and provenance. Use ComfyUI to make illustrations, original textures or concept footage. Label generated editorial illustrations clearly and use sourced footage for actual events.
2. Start with a supported workflow and verify the needed nodes, checkpoints, VRAM and licenses. Use a separate local workspace, start with a low-resolution still or short proof, then scale up after a valid result. Prefer built-in nodes when they meet the need.
3. Keep the editable workflow JSON. If automating with the API, export the API workflow separately and verify API endpoints against the installed server version. Record model identifiers, seed, sampler, steps and size. Keep secrets and personal inputs out of the exported graph.
4. For an image sequence, lock the seed policy, aspect ratio and camera across the sequence. Check for flicker and inconsistent text. Add precise labels, dates and numbers in the compositor.
5. Pass reviewed local files to the editor with the workflow, source and usage label. For PipelineX, preserve credit fields and confirm the visual matches the approved narration beat.

[ComfyUI repository](https://github.com/Comfy-Org/ComfyUI) · [ComfyUI documentation](https://docs.comfy.org/)
