---
name: spline
description: Build and edit 3D scenes live in the Spline 3d editor. Use when the user mentions Spline or asks for a 3D scene, object, animation made in Spline.
---

# Spline

One set of tools drives two Spline editors:

- **3D** (`3d_*` tools): scenes, objects, materials, lighting, cameras,
  animation and interactivity, authored in Spline's editor DSL.
- **2D design, "Hana"** (`2d_*` tools): websites, app screens, UI and
  posters, authored as an HTML + CSS subset that becomes a live Spline design.

Pick by what the user wants to end up with: a 3D scene → `3d_*`; a page or
screen → `2d_*`.

## Start

1. **Put an editor on screen.** In ChatGPT, call `spline_create_file`
   (`kind: "3d"` or `"2d"`) for something new, or `spline_open_file` for an
   existing file. It opens the Spline panel beside the chat, where the user
   watches you build. Call the scene tools right after; they wait for the
   editor to load.
2. **Read the authoring guide before you author.** 3D:
   `3d_load_skill("authoring-guide")`, then the further parts it names. 2D:
   `2d_load_skill("authoring-guide")` and `2d_load_skill("authoring-guide-2")`,
   plus any effect skill the design needs. The guides own the syntax and the
   quality bar; don't guess either.
3. **Ground yourself** with `3d_get_scene_mcp` or `2d_get_canvas_state`.

## Build, look, refine

Spline's own in-editor agent works in passes, and the results show it. Work
the same way:

- Build in steps (`3d_run_code`; `2d_reserve_frames` then `2d_write_html`).
- After each meaningful step, **look**: `3d_take_screenshot` (aim it with
  `3d_set_view`) or `2d_review_frame`. Check facts by re-reading the scene;
  judge looks from the image.
- **Refine at least twice** before you call it done: first composition,
  scale and framing; then materials, lighting and detail. Fix what the
  screenshot shows, not what you meant to build.
- Stop when the result meets the guide's quality bar, not when the first
  build runs without errors.

## Rules

- **One file per design.** Follow-up requests edit the open file; don't call
  `spline_create_file` again. If a create reports a file is already open,
  carry on in it.
- If a tool says no editor is open, open one (step 1) and retry. If it says
  the editor didn't finish loading, ask the user to check the Spline panel
  instead of creating another file.
- When you finish, tell the user the result is in the Spline panel (or their
  Spline tab) and what you built, so they can keep editing it themselves.
