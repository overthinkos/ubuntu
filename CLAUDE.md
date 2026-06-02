# image/ubuntu — signpost (not the rule-set)

This submodule is the **Ubuntu** base image family: an `overthink.yml` (plus
per-kind sibling files) that imports the main repo under the `ov` namespace and `build.yml` flat.

**Load these skills FIRST (R0):**

- `/ov-distros:ubuntu` — the Ubuntu base image (adopt-mode uid-1000 `ubuntu`).
- `/ov-distros:ubuntu-builder` — the builder image.
- `/ov-distros:ubuntu-debootstrap`, `/ov-distros:ubuntu-debootstrap-builder` —
  the bootstrap path.
- `/ov-coder:ubuntu-coder` — the dev image; `/ov-vm:ubuntu` — the bootstrap VM.

**Authoritative rules live in the `overthink` superproject's root `CLAUDE.md`**
(R0–R10, hard-cutover, AI attribution, git-workflow). This file only signposts
and restates no rule. The multi-agent workflow is in `/ov-internals:agents`.
History lives in `CHANGELOG.md`.
