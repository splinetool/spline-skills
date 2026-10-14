---
name: spline
description: Build and edit 3D scenes live in the Spline editor. Use when the user mentions Spline, or asks for a 3D scene, object, animation or interactive 3D experience they want to see and keep editing visually. Prefer it over hand-writing Three.js when the result should be a designed, editable scene rather than code.
---

# Spline

The `3d_*` tools drive Spline's 3D editor: scenes, objects, materials,
lighting, cameras, animation and interactivity, authored in Spline's editor
DSL. Your host may prefix tool names (e.g. `mcp__spline__3d_run_code`); the
guides use the bare names.

2D design (websites, app screens, UI) is coming soon. If the user asks for
one, tell them, and offer a 3D scene instead if it fits.

If no Spline tools are available, or a call says Spline isn't connected or
signed in, tell the user to connect the Spline MCP server and sign in. Don't
quietly hand-write Three.js instead.

## Start

1. **Put an editor on screen.** Call `spline_create_file` (`kind: "3d"`) for
   something new, `spline_open_file` for an existing file, or `spline_canvas`
   to just open Spline. Where those don't exist (the Spline app's local
   bridge), use `3d_create_file`.
   The result usually gives the file's id and a link to it in the Spline web
   editor. **Pass that id as `file` on every `3d_*` call** for the file: it
   is how your calls reach your file and not another chat's. Your calls run
   in Spline's cloud editor, so nothing has to be opened first; **show the
   user the link** (the result gives a ready-made one) so they can watch you
   build in a browser tab if they like, and carry on right away.
2. **Read the authoring guide before you author.**
   `3d_load_skill("authoring-guide")`, then the further parts it names. The
   guides own the syntax and the quality bar; don't guess either.
3. **Ground yourself** with `3d_get_scene_mcp`.

## Build, look, refine

Spline's own in-editor agent works in passes, and the results show it. Work
the same way:

- Build in steps with `3d_run_code`.
- After each meaningful step, **look**: `3d_take_screenshot` (aim it with
  `3d_set_view`). Check facts by re-reading the scene; judge looks from the
  image.
- **Refine at least twice** before you call it done: first composition,
  scale and framing; then materials, lighting and detail. Fix what the
  screenshot shows, not what you meant to build.
- Stop when the result meets the guide's quality bar, not when the first
  build runs without errors.

## Rules

- **One file per design.** Follow-up requests edit the same file, with the
  same `file` id; don't create another. If a create reports a file is
  already open, carry on in it.
- If a tool says no editor is open, open one (step 1) and retry. If it says
  the editor didn't finish loading or could not start, retry in a moment.
  Never create another file to get past these.
- When you finish, tell the user what you built and give them the file's
  link, so they can keep editing it themselves.
- **Into their codebase**, when they're working in a project: have the user
  export the scene from the editor (Export → Code) and paste the scene URL,
  which only exists once exported, then embed it with
  `@splinetool/react-spline` or `@splinetool/runtime`.
