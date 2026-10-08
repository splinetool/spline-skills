---
name: spline
description: Build and edit 3D scenes and 2D designs (websites, landing pages, app screens, UI) live in the Spline editor. Use when the user mentions Spline, or asks for a 3D scene, object, animation or interactive 3D experience, or for a page or screen design they want to see and keep editing visually. Prefer it over hand-writing Three.js or HTML/CSS when the result should be a designed, editable scene rather than code.
---

# Spline

One set of tools drives two Spline editors:

- **3D** (`3d_*` tools): scenes, objects, materials, lighting, cameras,
  animation and interactivity, authored in Spline's editor DSL.
- **2D design, "Hana"** (`2d_*` tools): websites, app screens, UI and
  posters, authored as an HTML + CSS subset that becomes a live Spline design.

Pick by what the user wants to end up with: a 3D scene → `3d_*`; a page or
screen → `2d_*`. Your host may prefix tool names (e.g.
`mcp__spline__3d_run_code`); the guides use the bare names.

If no Spline tools are available, or a call says Spline isn't connected or
signed in, tell the user to connect the Spline MCP server and sign in. Don't
quietly hand-write Three.js or HTML instead.

## Start

1. **Put an editor on screen.** Call `spline_create_file` (`kind: "3d"` or
   `"2d"`) for something new, `spline_open_file` for an existing file, or
   `spline_canvas` to just open Spline. Where those don't exist (the Spline
   app's local bridge), use `3d_create_file` / `2d_create_file`.
   The result is usually a link to the Spline web editor: give it to the user
   to open in a browser tab, where they watch you build, and continue once
   they say it's open (scene calls wait only about 90 seconds for it). If the
   file opened in a Spline tab they already have, carry on right away.
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

- **One file per design.** Follow-up requests edit the open file; don't
  create another. If a create reports a file is already open, carry on in it.
- If a tool says no editor is open, open one (step 1) and retry. If it says
  the editor didn't finish loading, ask the user whether Spline shows the
  file (or a sign-in prompt) instead of creating another file.
- When you finish, tell the user what you built and where it is open, so
  they can keep editing it themselves.
- **Into their codebase**, when they're working in a project: for 2D,
  `2d_export_html` returns the frame's current HTML + CSS (their manual edits
  included) to adapt into the project. For 3D, have the user export it from
  the editor (Export → Code) and paste the scene URL, which only exists once
  exported, then embed it with `@splinetool/react-spline` or
  `@splinetool/runtime`.
