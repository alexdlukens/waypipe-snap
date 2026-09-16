# waypipe snap — third-party build

> **AI-assisted:** This snap packaging (including this README) was
> produced with the help of AI tools and is maintained by @alexdlukens.
> Use at your own discretion.

A third-party Snap package of
[waypipe](https://gitlab.freedesktop.org/mstoeckl/waypipe/), a proxy for
Wayland protocol applications so they can be used remotely over an SSH
connection.

**Not produced, maintained, or endorsed by the upstream waypipe
author(s).** Packaging issues belong in this repository's issue tracker;
upstream bugs go to the
[upstream issue tracker](https://gitlab.freedesktop.org/mstoeckl/waypipe/-/issues).

## Install

Classic-confinement snap, built from the upstream git tree
(`snapcraft.yaml` sets the version as `<upstream version>+<git short hash>`):

```sh
sudo snap install ./waypipe_*.snap --dangerous --classic
```

## Build

Requires [snapcraft](https://snapcraft.io/docs/installing-snapcraft):

```sh
snapcraft
```

The build clones upstream waypipe from Git and enables the `video`, `dmabuf`,
`lz4`, `zstd`, and `gbmfallback` features. The `video` feature needs the
`ffmpeg-2404-sdk` build snap and, at runtime, the `ffmpeg-2404` content
provider snap (auto-installed via the declared plug).

## Notes

- **Classic confinement is deliberate** — waypipe execs arbitrary
  user-specified commands, runs host `ssh` with the user's identity, and
  creates sockets in `/tmp`/`XDG_RUNTIME_DIR` that non-snap peers must reach.
  None of that works strictly confined. The full case is in
  [rationale.md](rationale.md).
- This snap targets classic distro systems only (classic snaps are not
  installable on Ubuntu Core).
- **License:** GPL-3.0-or-later (waypipe-c is MIT); this snap redistributes
  the compiled upstream binary, and the full license texts are shipped in
  the snap as `/snap/waypipe/current/LICENSE.GPLv3` and
  `/snap/waypipe/current/LICENSE.MIT`.
