---
name: render-raea-video
description: Prototype GPU-rendered React and TypeScript video shots in Raea. Use for Rust and Bevy-backed motion graphics, deterministic 3D inserts, renderer evaluation, and footage handoff into PipelineX.
---

# Render Raea Video

1. Verify the target machine's adapter and the current Raea release and CLI help. Work in a separate Raea project, starting with a minimal known-good scene, a local asset and a short preview at the target aspect ratio.
2. Choose an FPS, dimensions, frame count, color treatment and camera path. Keep scene transforms driven by the render time and use a fixed random seed where available. Check the same frame after a forward seek and a backward seek.
3. Compare preview and recorded frames for layout, shader output and asset loading. Record the version, GPU, actual frame rate, render time and any fallback used. Treat performance estimates as device-specific.
4. Export a local clip or supported frame sequence for PipelineX. Probe the file, confirm alpha if needed and keep a still or intermediate clip as a review artifact. Preserve the existing production renderer selection.
5. Check the repository license for the version you use. Raea documents FSL-1.1-ALv2 terms and a restriction for competing products. Treat vendor integration and code redistribution separately from an isolated prototype.

[Raea](https://github.com/shinyobjectz/raea)
