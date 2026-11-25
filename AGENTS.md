# Agent rules

This fork builds Godot at double precision from a pinned commit of `V-Sekai-fire/entities-godot-4.7` (4.7.2-stable plus our bug-fix backports). Its one rule: **the Godot commit never changes here.** A change to Godot reaches it as a pull request to `entities-godot-4.7`, and then a new pinned SHA here.

- Godot is built from that pinned commit, checked out by its full SHA. No patch, no extra commit and no added file goes into the Godot tree. `.github/workflows/double.yml` refuses to build unless `git rev-parse HEAD` is the pinned SHA and `git status --porcelain` is empty, and checks the tree again after the build.
- `godotengine/godot-build-scripts` is used as published, at a pinned commit: the workflow takes its `OPTIONS` lines and its dependency URLs from it.
- Every change lives here, in the containers: `Dockerfile.linux` and `Dockerfile.windows` set `SCONSFLAGS="precision=double"`, which scons reads on every call.
- A new backport or Godot release means a new pinned SHA (and, for a new release, the matching `build-containers` and `godot-build-scripts` branch), never an edit to Godot here.
