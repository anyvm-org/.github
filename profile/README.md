<div align="center">

# Run any VM anywhere

**One Python file boots 17 guest operating systems across 7 CPU architectures -- on Linux, macOS and Windows.**

[![PyPI](https://img.shields.io/pypi/v/anyvm.py)](https://pypi.org/project/anyvm.py/)
[![Python](https://img.shields.io/pypi/pyversions/anyvm.py)](https://pypi.org/project/anyvm.py/)
[![Test](https://github.com/anyvm-org/anyvm/actions/workflows/test.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/test.yml)

[anyvm.org](https://anyvm.org) &nbsp;&middot;&nbsp; [anyvm repository](https://github.com/anyvm-org/anyvm) &nbsp;&middot;&nbsp; [all repositories](https://github.com/orgs/anyvm-org/repositories)

</div>

---

Need to test your code on FreeBSD? On NetBSD/sparc64? On Solaris, Haiku, or
Plan 9? One command:

```bash
anyvm --os freebsd -- uname -a
```

`anyvm.py` is a single Python file with no third-party dependencies. It picks a
prebuilt, CI-verified guest image, downloads it, configures QEMU with defaults
that actually work for that guest and that architecture, boots it, and drops
you into an SSH session -- or runs your command inside the guest and exits.
No libvirt, no Vagrant, no VirtualBox, and no image to build yourself.

## Start in 30 seconds

```bash
pip install anyvm.py            # or: brew install anyvm-org/tap/anyvm
anyvm --os freebsd
```

Prefer a container? `docker run --rm -it ghcr.io/anyvm-org/anyvm:latest --os freebsd`

Or launch straight into a ready-made cloud environment:

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/anyvm-org/anyvm)
<a href="https://shell.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https%3A%2F%2Fgithub.com%2Fanyvm-org%2Fanyvm&cloudshell_tutorial=.cloudshell%2Ftutorial.md&show=terminal&ephemeral=true&cloudshell_print=.cloudshell%2Fconsole.md" target="_blank" rel="noopener noreferrer"><img src="https://gstatic.com/cloudssh/images/open-btn.svg" alt="Try it Now in Cloud Shell"></a>

A few more things it does out of the box:

```bash
# Pick a release and a CPU architecture
anyvm --os netbsd --release 11.0 --arch sparc64

# Share a host folder with the guest
anyvm --os freebsd -v "$PWD:/data"

# Boot a desktop image and open it in your browser
anyvm --os openbsd --release 7.9-xfce
```

## Why AnyVM

- **One file, standard library only.** Nothing to compile, nothing to vendor.
  Copy `anyvm.py` around and it works.
- **Images are prebuilt and boot-tested.** Every image in the matrix below is
  produced and verified by its own builder repository in this organization, on
  every release -- so a green check means that guest really boots on that
  architecture today.
- **Acceleration is automatic.** KVM, HVF or WHPX is detected and used when
  available, with a clean fall back to TCG emulation when it is not.
- **Folder sync that works everywhere.** Six backends (`rsync`, `sshfs`,
  `nfs`, `sys-nfs`, `scp`, `9p`), including a bundled pure-Python NFS server so
  even Windows and macOS hosts can export a directory without root.
- **A graphical console in your browser.** The built-in VNC web UI starts by
  default, with clipboard, fullscreen, optional password, and one-flag public
  tunnelling via `--remote-vnc`.
- **Desktops, not just shells.** XFCE, GNOME, KDE, MATE, LXQt and more ship as
  ready-to-boot desktop images for several guests.

## Guest support

| Guest | x86_64 | aarch64 (arm64) | riscv64 | powerpc64 | sparc64 | s390x | loongarch64 | Builder |
|-------|--------|-----------------|---------|-----------|---------|-------|-------------|---------|
| Ubuntu<br>[![Test Ubuntu](https://github.com/anyvm-org/anyvm/actions/workflows/ubuntu.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/ubuntu.yml) | ✅ | ✅ | ✅ | ✅ | — | ✅ | — | [![Build Ubuntu](https://github.com/anyvm-org/ubuntu-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/ubuntu-builder) |
| OpenEuler<br>[![Test openEuler](https://github.com/anyvm-org/anyvm/actions/workflows/openeuler.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/openeuler.yml) | ✅ | ✅ | ✅ | — | — | — | ✅ | [![Build openEuler](https://github.com/anyvm-org/openeuler-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/openeuler-builder) |
| FreeBSD<br>[![Test FreeBSD](https://github.com/anyvm-org/anyvm/actions/workflows/freebsd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/freebsd.yml) | ✅ | ✅ | ✅ | ✅ | — | — | — | [![Build FreeBSD](https://github.com/anyvm-org/freebsd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/freebsd-builder) |
| OpenBSD<br>[![Test OpenBSD](https://github.com/anyvm-org/anyvm/actions/workflows/openbsd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/openbsd.yml) | ✅ | ✅ | ✅ | — | ✅ | — | — | [![Build OpenBSD](https://github.com/anyvm-org/openbsd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/openbsd-builder) |
| NetBSD<br>[![Test NetBSD](https://github.com/anyvm-org/anyvm/actions/workflows/netbsd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/netbsd.yml) | ✅ | ✅ | ✅ | — | ✅ | — | — | [![Build NetBSD](https://github.com/anyvm-org/netbsd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/netbsd-builder) |
| DragonFlyBSD<br>[![Test DragonflyBSD](https://github.com/anyvm-org/anyvm/actions/workflows/dragonflybsd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/dragonflybsd.yml) | ✅ | — | — | — | — | — | — | [![Build DragonflyBSD](https://github.com/anyvm-org/dragonflybsd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/dragonflybsd-builder) |
| MidnightBSD<br>[![Test MidnightBSD](https://github.com/anyvm-org/anyvm/actions/workflows/midnightbsd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/midnightbsd.yml) | ✅ | — | — | — | — | — | — | [![Build MidnightBSD](https://github.com/anyvm-org/midnightbsd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/midnightbsd-builder) |
| GhostBSD<br>[![Test GhostBSD](https://github.com/anyvm-org/anyvm/actions/workflows/ghostbsd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/ghostbsd.yml) | ✅ | — | — | — | — | — | — | [![Build GhostBSD](https://github.com/anyvm-org/ghostbsd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/ghostbsd-builder) |
| NextBSD<br>[![Test NextBSD](https://github.com/anyvm-org/anyvm/actions/workflows/nextbsd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/nextbsd.yml) | ✅ | — | — | — | — | — | — | [![Build NextBSD](https://github.com/anyvm-org/nextbsd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/nextbsd-builder) |
| Solaris<br>[![Test Solaris](https://github.com/anyvm-org/anyvm/actions/workflows/solaris.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/solaris.yml) | ✅ | — | — | — | — | — | — | [![Build Solaris](https://github.com/anyvm-org/solaris-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/solaris-builder) |
| OmniOS<br>[![Test OmniOS](https://github.com/anyvm-org/anyvm/actions/workflows/omnios.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/omnios.yml) | ✅ | — | — | — | — | — | — | [![Build OmniOS](https://github.com/anyvm-org/omnios-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/omnios-builder) |
| OpenIndiana<br>[![Test OpenIndiana](https://github.com/anyvm-org/anyvm/actions/workflows/openindiana.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/openindiana.yml) | ✅ | — | — | — | — | — | — | [![Build OpenIndiana](https://github.com/anyvm-org/openindiana-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/openindiana-builder) |
| Tribblix<br>[![Test Tribblix](https://github.com/anyvm-org/anyvm/actions/workflows/tribblix.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/tribblix.yml) | ✅ | — | — | — | — | — | — | [![Build Tribblix](https://github.com/anyvm-org/tribblix-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/tribblix-builder) |
| Haiku<br>[![Test Haiku](https://github.com/anyvm-org/anyvm/actions/workflows/haiku.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/haiku.yml) | ✅ | — | — | — | — | — | — | [![Build Haiku](https://github.com/anyvm-org/haiku-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/haiku-builder) |
| BlissOS (Android)<br>[![Test BlissOS](https://github.com/anyvm-org/anyvm/actions/workflows/blissos.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/blissos.yml) | ✅ | — | — | — | — | — | — | [![Build BlissOS](https://github.com/anyvm-org/blissos-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/blissos-builder) |
| GNU Hurd (Debian)<br>[![Test Hurd](https://github.com/anyvm-org/anyvm/actions/workflows/hurd.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/hurd.yml) | ✅ (also i386) | — | — | — | — | — | — | [![Build Hurd](https://github.com/anyvm-org/hurd-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/hurd-builder) |
| Plan 9 (9front)<br>[![Test Plan 9](https://github.com/anyvm-org/anyvm/actions/workflows/plan9.yml/badge.svg)](https://github.com/anyvm-org/anyvm/actions/workflows/plan9.yml) | ✅ | — | — | — | — | — | — | [![Build Plan 9](https://github.com/anyvm-org/plan9-builder/actions/workflows/build.yml/badge.svg)](https://github.com/anyvm-org/plan9-builder) |

Hosts: Linux, macOS and Windows, natively on x86_64 and arm64. See the
[anyvm README](https://github.com/anyvm-org/anyvm#5-host-support) for the full
host-to-guest support table.

## Also powering vmactions

The same images run inside the [vmactions](https://github.com/vmactions) GitHub
Actions -- `freebsd-vm`, `openbsd-vm`, `netbsd-vm`, `solaris-vm` and friends --
which execute your CI steps inside a real BSD or illumos guest on GitHub's
Linux runners.

## What's in this organization

**Core**

| Repository | What it is |
|---|---|
| [anyvm](https://github.com/anyvm-org/anyvm) | The launcher: one Python file, no dependencies, every guest and architecture above. |
| [docker](https://github.com/anyvm-org/docker) | Run any guest inside a Docker container -- disposable environments for CI and throwaway work. |
| [homebrew-tap](https://github.com/anyvm-org/homebrew-tap) | `brew install anyvm-org/tap/anyvm`, with QEMU pulled in as a dependency. |

**AI agents**

| Repository | What it is |
|---|---|
| [mcp](https://github.com/anyvm-org/mcp) | MCP server -- let Claude Code, Copilot or any MCP client boot and drive VMs for you. |
| [anyvm-skill](https://github.com/anyvm-org/anyvm-skill) | Agent skill file that teaches an assistant to use anyvm from plain-language requests. |

**Images**

[base-builder](https://github.com/anyvm-org/base-builder) is the single
template every image builder is generated from. Each guest then gets its own
builder repository, which builds, boots and publishes that guest's images:

[blissos](https://github.com/anyvm-org/blissos-builder) &middot;
[dragonflybsd](https://github.com/anyvm-org/dragonflybsd-builder) &middot;
[freebsd](https://github.com/anyvm-org/freebsd-builder) &middot;
[ghostbsd](https://github.com/anyvm-org/ghostbsd-builder) &middot;
[haiku](https://github.com/anyvm-org/haiku-builder) &middot;
[hurd](https://github.com/anyvm-org/hurd-builder) &middot;
[midnightbsd](https://github.com/anyvm-org/midnightbsd-builder) &middot;
[netbsd](https://github.com/anyvm-org/netbsd-builder) &middot;
[nextbsd](https://github.com/anyvm-org/nextbsd-builder) &middot;
[omnios](https://github.com/anyvm-org/omnios-builder) &middot;
[openbsd](https://github.com/anyvm-org/openbsd-builder) &middot;
[openeuler](https://github.com/anyvm-org/openeuler-builder) &middot;
[openindiana](https://github.com/anyvm-org/openindiana-builder) &middot;
[plan9](https://github.com/anyvm-org/plan9-builder) &middot;
[solaris](https://github.com/anyvm-org/solaris-builder) &middot;
[tribblix](https://github.com/anyvm-org/tribblix-builder) &middot;
[ubuntu](https://github.com/anyvm-org/ubuntu-builder)

**Infrastructure**

| Repository | What it is |
|---|---|
| [nfsd](https://github.com/anyvm-org/nfsd) | A user-space NFSv3/v4.0/v4.1/v4.2 server in one pure-Python file. Powers `--sync nfs` on any host, no root and no kernel module. |

---

<div align="center">

[anyvm.org](https://anyvm.org) &nbsp;&middot;&nbsp;
[PyPI](https://pypi.org/project/anyvm.py/) &nbsp;&middot;&nbsp;
[All repositories](https://github.com/orgs/anyvm-org/repositories) &nbsp;&middot;&nbsp;
infogh@anyvm.org

</div>
