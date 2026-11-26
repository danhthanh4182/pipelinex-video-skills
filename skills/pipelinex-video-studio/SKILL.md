---
name: pipelinex-video-studio
description: Produce and review news, explainers, Shorts, and motion inserts in PipelineX. Use when working with a PipelineX video job, editor MCP, timeline, voice, render, fact-check, or publishing handoff across Remotion, HyperFrames, and iArt.
---

# PipelineX Video Studio

1. Open the [PipelineX repository](https://github.com/danhthanh4182/PipelineX). Read its current `AGENTS.md`, `PIPELINEX.md`, and `renderer/templates/README.md` if present. For a job, start with its status, variant, current edit state, and channel profile.
2. Keep the editorial contract. Cite claims against the dossier and fact-check, trace visuals to their credits and licenses, and follow the channel's configured language. Default to the user's requested language for briefs outside production. Preserve the human publishing decision.
3. Use the existing editor workflow for approved edits. Before repeating a stage, find its first stale input. For wording changes, keep fact-check ahead of assets and voice. For a visual-only change, preserve existing narration timing when it still matches. For renderer trials, use a separate directory under `renderer/templates/out/`.
4. Use Remotion for the production long video, Short, and thumbnail. Use the HyperFrames exporter for a review cut made from the same timed audio and copy. Use iArt for approved motion inserts, starting with a brief that can be reviewed without a request to the vendor. Keep its credits and inputs outside the free model chain.
5. Inspect frames at the hook, a beat boundary, and the end. Confirm font coverage, audio, aspect ratio, and credits. Compare exact numbers, units, and as-of dates to the sources. Deliver the review artifact and list any pending editorial decisions.

## Optional workflows

- Use `$analyze-video-references` to extract design principles and plan original shots.
- Use `$build-video-effects` for EffectCraft compositions or PixelFX overlays, `$generate-comfyui-video-assets` for generated illustrations, and `$build-3d-video-shots` for Three.js and Blender inserts.
- Use `$build-code-explainers` for narrated, sourced explainers and `$direct-continuous-launch-videos` for product reveals, continuity review and timecoded feedback.
- Use `$produce-screen-demo-video` for app footage and `$render-raea-video` for GPU-rendered inserts in a separate preview project.
- Use `$deliver-video-with-ffmpeg` to conform and verify MP4s. Use the upstream Remotion and GSAP guidance linked in the template README when working on either engine.

For a dry run with sample media, follow the template README. For a real production job, confirm the appropriate review gates before requesting any publish action.
