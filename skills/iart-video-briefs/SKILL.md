---
name: iart-video-briefs
description: Write reusable iArt.ai motion graphics briefs for launch promos, kinetic typography, and chart inserts. Use when preparing iArt prompts, CSV or brand asset instructions, or a user-authorized iArt REST or MCP render.
---

# iArt Video Briefs

1. Start with a reviewable brief. Include purpose, aspect ratio, target length, language, exact on-screen copy, approved colors and asset names, timed scenes, and narration mode. For PipelineX, start from `renderer/templates/iart/` in the [project repository](https://github.com/danhthanh4182/PipelineX).
2. Give each scene one visual job and hold the final frame long enough to read. For exact data, provide the original approved CSV with the source, unit, and date range. Preserve missing observations and verify labels and digits after rendering.
3. Use `voiceover: false` for a graphics-only request. For a real voice, collect the cleared recording and specify its use in the brief. Check Vietnamese accents and proper names when relevant.
4. Use the official editor or documented MCP/REST route. Creation and revisions consume credits. Submit them when the user has authorized the charge and supplied or connected access. Send only approved assets with secrets, IDs, and private information removed. Preserve the provider's video ID and poll at the documented interval if asked to complete a render. If the create request has an ambiguous outcome, look up the existing job before retrying.
5. Inspect the resulting MP4 against the approved copy and data. Preserve its edit link if present. When used with PipelineX, hand back the reviewed clip for an editorial insert and preserve the existing fact-check and publishing steps.

[iArt API reference](https://www.iart.ai/docs/api) · [MCP setup](https://www.iart.ai/docs/mcp)
