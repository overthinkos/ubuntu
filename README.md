# overthinkos/ubuntu

The **Ubuntu image family** for [OpenCharly](https://github.com/overthinkos/overthink),
split into its own repository and mounted as a git submodule at `box/ubuntu`
of the main repo.

## What's here

| Kind | Entries |
|---|---|
| `image:` | `ubuntu` (base), `ubuntu-builder`, `ubuntu-coder`, `ubuntu-debootstrap`, `ubuntu-debootstrap-builder` |
| `vm:` | `ubuntu-debootstrap` (bootstrap-from-scratch via debootstrap) |
| `check:` | `check-ubuntu-debootstrap-vm` (disposable bootstrap-VM bed) |

## Composition by reference — nothing is vendored

This repo contains **no layers and no build-config of its own**. Everything is
pulled from `github.com/overthinkos/overthink` by **github reference**:

- every layer in `box.yml` is an `@github.com/overthinkos/overthink/candy/<name>:<tag>` ref;
- the shared build-config (`build.yml` — distro/builder/init) is a remote
  `import:` in `charly.yml`. Ubuntu is deb-family: `distro.ubuntu` is
  `inherits: debian`, and the single remote `build.yml` carries BOTH the
  `ubuntu` and `debian` distro configs, so the inheritance resolves with no
  extra include. It also carries the `deb` format template and the
  `debootstrap` builder template.

The `ubuntu` base roots at the upstream docker.io `ubuntu:24.04` image directly
(the `ubuntu-debootstrap-builder` is `base: debian:13`, since debootstrap is a
Debian tool), so this repo needs **no remote base include**. All references pin
to a single tag of the upstream repo, so a build is reproducible. There is
exactly one definition of every layer — no duplication.

## No coupling with main

Nothing in the main `opencharly` repo consumes any Ubuntu image (no
`base: ubuntu` image stays in main), so there is **no main ↔ ubuntu coupling**:
the only edge is `ubuntu → main` (this repo pulls layers + `build.yml`). Main
pulls nothing back. The image DAG is acyclic
(`ubuntu-coder → ubuntu → docker.io/ubuntu:24.04`;
`ubuntu-debootstrap → ubuntu-debootstrap-builder → docker.io/debian:13`).

## Build

```bash
# Inside the submodule (the build verb defaults to charly.yml):
charly box build ubuntu

# From the parent opencharly repo:
charly -C box/ubuntu box build ubuntu

# Standalone, against the published repo:
charly --repo overthinkos/ubuntu box build ubuntu
```

The first build resolves the upstream github references into
`~/.cache/charly/repos/` and materializes the referenced layers under
`.build/_layers/`.

## debootstrap-from-scratch (`ubuntu-debootstrap` / `check-ubuntu-debootstrap-vm`)

`ubuntu-debootstrap` builds an Ubuntu rootfs from scratch via `debootstrap`
inside the privileged `ubuntu-debootstrap-builder` container (`from:
builder:debootstrap`). `check-ubuntu-debootstrap-vm` boots that rootfs under
libvirt/QEMU and carries `disposable: true`, so `charly -C box/ubuntu update
check-ubuntu-debootstrap-vm` rebuilds it unattended.

## Requirements

A build of any image here fetches from the upstream repo, so it needs network
access and a `charly` recent enough to understand the config's schema version
(`charly` hard-fails with an "update charly" message if the config is newer than the
binary supports).

---
*Assisted-by: Claude*
