# box/ubuntu — signpost (not the rule-set)

This submodule is the **Ubuntu** base image family: a `charly.yml` (plus
per-kind sibling files) that imports the main repo under the `charly` namespace and `build.yml` flat.

**Load these skills FIRST (R0):**

- `/charly-distros:ubuntu` — the Ubuntu base image (adopt-mode uid-1000 `ubuntu`).
- `/charly-distros:ubuntu-builder` — the builder image.
- `/charly-distros:ubuntu-debootstrap`, `/charly-distros:ubuntu-debootstrap-builder` —
  the bootstrap path.
- `/charly-coder:ubuntu-coder` — the dev image; `/charly-vm:ubuntu` — the bootstrap VM.

**Authoritative rules live in the `opencharly` superproject's root `CLAUDE.md`**
(R0–R10, hard-cutover, AI attribution, git-workflow). This file only signposts
and restates no rule. The multi-agent workflow is in `/charly-internals:agents`.
History lives in `CHANGELOG.md`.
