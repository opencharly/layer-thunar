# layer-thunar

Thunar file manager for a Sway desktop container, bound to `$mod+e`.

The `thunar` candy installs the [Thunar](https://docs.xfce.org/xfce/thunar/start)
Xfce file manager (the Fedora RPM is named `Thunar` with a capital T, which
provides the lowercase `thunar` that dnf installs by; the binary lands at
`/usr/bin/thunar`) and drops a Sway `config.d` snippet that binds `$mod+e` to
launch it. It is the file browser used by the `sway-desktop` composition.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `thunar` |
| Package | `thunar` (Fedora RPM `Thunar`) |
| Binary | `/usr/bin/thunar` |
| Requires | `pod-sway` |
| Sway binding | `$mod+e exec thunar` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list — typically
transitively through the `sway-desktop` composition:

```yaml
my-desktop-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-thunar:v2026.243.0410'
```

Inside the desktop session, press `$mod+e` to launch Thunar, or run it directly:

```bash
thunar
```

The candy's `plan:` asserts the binary at `/usr/bin/thunar`, the package
registered in the package database, the drop-in at
`~/.config/sway/config.d/thunar.conf`, and that the drop-in contains the
`bindsym $mod+e exec thunar` line.

## Layout

- `charly.yml` — the `thunar:` candy entity (the `require:`, the `copy:` plan
  steps, the `check:` assertions) and the embedded `thunar-skill:` skill entity.
- `thunar.conf` — the Sway `config.d` drop-in copied into the user config.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:thunar`
- `/charly-selkies:sway` — compositor dependency
- `/charly-selkies:sway-desktop` — composition that includes this candy
- `/charly-selkies:xfce4-terminal` — terminal emulator (also in `sway-desktop`)
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
