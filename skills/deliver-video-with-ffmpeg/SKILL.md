---
name: deliver-video-with-ffmpeg
description: Inspect, conform and export videos with FFmpeg and FFprobe. Use for PipelineX deliverables, codec and audio checks, horizontal and vertical MP4, captions and alpha overlays.
---

# Deliver Video with FFmpeg

1. Probe inputs and record codec, dimensions, display aspect ratio, FPS, duration and audio streams. Inspect the first frame, transitions, the last frame and the audio mix.
2. Preserve intended framing. When source and target ratios differ, pick a deliberate crop or pad after inspecting subject and subtitle placement. Preserve the source FPS unless the deliverable specifies another rate.
3. For a normal MP4 that already has the right geometry, use the tested encoding example below. Keep audio optional for silent previews. Save to a new file and validate before replacing a delivery artifact.
4. For overlays, keep an alpha-capable source such as ProRes 4444 or an RGBA PNG sequence until compositing. Confirm the subscriber's format and editor can import it. For subtitles, deliver a UTF-8 SRT when the platform can accept it and verify Vietnamese diacritics in rendered text.
5. Decode the complete output with FFmpeg and probe the final streams. For PipelineX, attach the deliverable to the existing review handoff with the renderer, variant and observed specs.

```sh
ffprobe -v error -show_streams -show_format -of json "input.mp4"
ffmpeg -n -i "input.mp4" -map 0:v:0 -map "0:a:0?" -c:v libx264 -crf 18 -pix_fmt yuv420p -c:a aac -b:a 160k -movflags +faststart "delivery.mp4"
ffmpeg -v error -xerror -i "delivery.mp4" -f null -
```

[FFmpeg](https://github.com/FFmpeg/FFmpeg) · [FFmpeg documentation](https://ffmpeg.org/documentation.html)
