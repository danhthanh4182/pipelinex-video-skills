---
name: remotion-video-templates
description: Build and adapt React and TypeScript video compositions using Remotion. Use for reusable JSON-driven news videos, Shorts, explainers, product videos, animated data, captions, or CLI renders.
---

# Remotion Video Templates

1. Inspect the project's Remotion version, registration entry point, compositions, and asset paths. Keep existing package versions aligned. For PipelineX, use `renderer/src/index.ts` with `NewsVideo`, `ShortVideo`, or the `Thumbnail` still. Use the sample timeline and `renderer/templates/README.md` for a dry run.
2. Put editable copy, brand, visual references, and timing in JSON props. Use frame-derived values (`useCurrentFrame`, `interpolate`, `spring`) and consume the same input for preview and render. Use `calculateMetadata` when FPS, geometry, or duration comes from props. Round absolute start and end boundaries consistently before computing sequence spans.
3. Resolve local media through `staticFile` and verify paths with the selected public directory. For licensed voice recordings or TTS, align captions to word marks where available. Verify accents, line wraps, and the safe area in the actual target aspect ratio.
4. Preview representative frames. Render through the existing project command, or use `remotion render <entry> <composition> <output> --props=<json-file>`. Use a props file in PowerShell. Check codec, duration, dimensions, and audio with FFprobe, then inspect both the hook and the final hold.
5. For charts, read labeled data rather than estimating values from an image. Keep scale and units stable through animation. For a variant, adapt the layout and caption placement while reusing the data.

[Remotion rendering](https://www.remotion.dev/docs/render) · [Dynamic metadata](https://www.remotion.dev/docs/dynamic-metadata)
