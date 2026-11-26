---
name: build-video-effects
description: Build reusable motion graphics, overlays and pixel effects using EffectCraft or PixelFX. Use for layer compositing, alpha delivery, transitions, sprites, kinetic titles and effects in PipelineX.
---

# Build Video Effects

1. Define the effect's role, duration, FPS, pixel dimensions, transparency, palette and expected host renderer. Preview it over the actual footage and next to captions before choosing intensity.
2. Use EffectCraft for a layered composition with keyframes, masks or a render queue. Preserve the editable project and local media. Check the installed CLI's help before scripting it. Choose a PNG sequence or ProRes 4444 for transparent interchange if supported by the next renderer.
3. Use PixelFX as a source of implementations and ideas for pixel-art overlays. Read the chosen effect's source and license first. Port the smallest applicable effect with its notices when required. Use a fixed seed and frame time for particles, keep a fixed pixel grid and use nearest-neighbor scaling for sprite artwork.
4. For Remotion or HyperFrames, avoid wall-clock timers as the source of animation state. Test first, middle and last frames plus a backward seek. Check that transparent pixels remain clean over light and dark backgrounds.
5. For PipelineX, export the effect as a separate insert and map it to an approved beat. Record the source, license, time range and alpha format. Deliver the editable source with a rendered test clip.

[EffectCraft](https://github.com/storytold/effectcraft) · [PixelFX](https://github.com/patch-gg/pixelfx)
