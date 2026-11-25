# Agent rules

This fork builds stock Godot at double precision. Its one rule: **the Godot commit never changes.**

- Godot is built from the commit of a stable release tag, checked out by its full SHA. No patch, no extra commit and no added file goes into the Godot tree. `.github/workflows/double.yml` refuses to build unless `git rev-parse HEAD` is the pinned SHA and `git status --porcelain` is empty, and checks the tree again after the build.
- `godotengine/godot-build-scripts` is used as published, at a pinned commit: the workflow takes its `OPTIONS` lines and its dependency URLs from it.
- Every change lives here, in the containers: `Dockerfile.linux` and `Dockerfile.windows` set `SCONSFLAGS="precision=double"`, which scons reads on every call.
- A new Godot release means a new pinned tag and SHA (and the matching `build-containers` and `godot-build-scripts` branch), never an edit to Godot.
