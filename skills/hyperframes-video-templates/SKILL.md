---
name: hyperframes-video-templates
description: Build editable HTML, CSS, and GSAP videos with HeyGen HyperFrames. Use for kinetic titles, product promos, captions, and standalone review cuts from PipelineX timelines.
---

# HyperFrames Video Templates

1. For PipelineX, use the exporter under `renderer/templates/`. Give it the timeline file and a new output directory. Select `long` for 16:9 or `short` for 9:16. It uses the original beat audio and emits timed editorial cards. Use its README for exact commands.
2. For an independent HTML composition, place timed clips in a root with `data-composition-id`, `data-start`, `data-duration`, `data-width` and `data-height`. Give overlapping media distinct tracks and explicitly time audio clips. Register a paused GSAP timeline at `window.__timelines[compositionId]` and make it seekable at arbitrary times. Package fonts and runtime assets locally where possible.
3. Verify that scene and beat offsets are added exactly once. Derive captions from word timestamps. Treat evenly distributed fallback captions as estimates pending review. Use layout bounds suited to the aspect ratio, especially around social platform overlays.
4. Run the installed CLI's `lint`, `snapshot` and `render` commands. Use flag help for that installed version. Check frames at a transition and under the longest title, then probe the MP4 and listen to its audio.
5. Save the editable project with the sample MP4 when the user requests a template. Keep review renders independent of any live publish job.

[HyperFrames documentation](https://hyperframes.heygen.com/introduction) · [CLI reference](https://hyperframes.app/docs/5-packages/cli)
