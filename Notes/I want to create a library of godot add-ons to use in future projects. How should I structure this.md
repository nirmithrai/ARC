Here’s the short, punchy version:

- **Use separate repos per brick.** One repo = one addon (`addons/brick.<name>`). Tag releases, keep a terse CHANGELOG.
- **Prefer Git subtrees for games.** Self-contained projects, simple CI, easy updates with `git subtree pull`. Use submodules only if your team already loves them.
- **Repo layout:** no `project.godot` near the addon. Put the addon in `addons/brick.<name>/…` and a testable **demo project** in `/demo` that contains `project.godot`. Optionally maintain a `dist` branch containing only the addon for ultra-clean consumption.
- **Edit where the truth lives.**
    - Generic improvement? Change the **brick repo**, tag, then pull into games via subtree.
    - Project-specific tweak? Extend/compose in the **game** (adapters, subclasses, config), don’t fork the brick.
    - If two games truly diverge long-term: add feature flags/config; else maintain variant branches or split into a second brick.
- **Make bricks self-installing.** In `EditorPlugin.enable()`, auto-create InputMap actions (and autoloads if needed). Avoid manual project setup steps.
- **Name everything with a prefix.** Classes, actions, autoloads: `BrickFPS_*`, `brick_fps_*` to prevent collisions.
- **API via signals, not tight coupling.** Emit events; let games wire behavior. Provide small adapters for common integrations.
- **Pin versions.** Games reference brick tags (`vX.Y.Z`)—no “latest”. Document breaking changes.
- **Basic CI sanity:** headless parse on push, optional lint/format, tiny demo scene to catch regressions.

That’s the whole system: versioned “LEGO bricks,” pulled into any project cleanly, with low-friction updates and room for per-game customization without forking chaos.