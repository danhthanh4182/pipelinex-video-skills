---
name: build-3d-video-shots
description: Design 3D video inserts using Three.js or the community MCP for Blender. Use for product turns, camera moves, spatial explainers, GLB export, and frame-based capture in Remotion or HyperFrames.
---

# Build 3D Video Shots

1. Define the frame size, camera path, subject, lighting, aspect ratio, FPS and duration. Save a first-frame reference. Ask the viewer to track one object or movement at a time.
2. Use Three.js for procedural scenes that belong in a browser composition. Use the render frame as the input for transforms and camera state. Ensure local textures and meshes are ready before capture. Seek in forward and reverse order and verify the same frame renders the same way.
3. Use Blender for model, material and lighting work or offline render passes. If the community MCP is already connected, inspect the active scene before edits and work on a duplicate or a dedicated scene. Use the project's version-specific setup guide if the user requests connection.
4. Use GLB for a browser handoff and check axis, units, texture paths and material support. Use a rendered frame sequence or compatible clip when the edit does not need editable 3D. Confirm alpha and color treatment in the compositor.
5. For PipelineX, attach reviewed local media to the appropriate visual beat and record asset provenance. Check edges, overlays and text against the actual camera motion at target resolution.

[Three.js](https://github.com/mrdoob/three.js) · [Community MCP for Blender](https://github.com/ahujasid/mcp-for-blender)
