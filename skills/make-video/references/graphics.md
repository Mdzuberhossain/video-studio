# Graphical elements (AntV)

Use AntV for anything data- or diagram-shaped inside a scene. Plain HTML/CSS stays the default for text and layout.

| Need | Package |
|---|---|
| Charts (bar, line, area, pie, KPI growth) | `@antv/g2` |
| Graphs, flows, architecture diagrams, org/relationship maps | `@antv/g6` |
| Infographics (lists, steps, comparisons, timelines) | `@antv/infographic` |
| Maps | `@antv/l7` |

## Rules for frame-by-frame rendering

HyperFrames captures frames by seeking time. AntV's own animations run on wall-clock time, so they will skip or stutter in the render.

1. **Turn AntV's animation off.** In G2 set `animate: false`, and in G6 set `animation: false`.
2. **Animate through the HyperFrames timeline instead,** for example a clip-path wipe to reveal bars or lines, opacity or scale on nodes, or counters driven by timeline progress. Then preview and render match frame for frame.
3. **Finish drawing before the scene starts.** Await `chart.render()` / `graph.render()` and only then signal ready, following the HyperFrames skill's way of waiting for async content.
4. **Pin exact versions.** Either install with npm into the project or load from a CDN with an exact version (e.g. `https://unpkg.com/@antv/g2@<x.y.z>/dist/g2.min.js`). An unpinned version can render a different video next month.
5. **Use real data from the repo or the brief.** If none exists, ask the user. Never invent numbers for a launch or customer video.
6. **Size charts to the composition** (fixed `width`/`height` in px, not `autoFit`), so every platform cut lays out the same. Match the brand's colours and font by passing them through the `theme`.

Check the installed version's docs for option names before you write code. G2 v5 and G6 v5 changed many APIs from v4.
