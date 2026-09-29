# AGENTS.md — layer-thunar

Standalone candy repo for the `thunar` layer — the Thunar Xfce file manager
installed and bound to `$mod+e` in a Sway desktop. The candy lives in
`charly.yml` at the repo root: the `require:` on `pod-sway`, the `copy:` plan
steps, the `check:` assertions, and the embedded `skill:` entity projected into
the marketplace corpus as `/charly-selkies:thunar`.

Canonical files:

- `charly.yml` — the `thunar:` candy entity and the `thunar-skill:` skill entity.
- `thunar.conf` — the Sway `config.d` drop-in copied to
  `~/.config/sway/config.d/thunar.conf`; its `bindsym $mod+e exec thunar` line
  is asserted by a check.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:thunar` — the owning skill. The package, the Sway binding, and
  the desktop composition. Load before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, service declarations). Load before editing any entity field or plan
  step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence. The `package:`
  check maps Fedora's capital-T `Thunar`; keep that `package_map` in sync with
  the `distro:` arm.
- The drop-in content check asserts the exact `bindsym $mod+e exec thunar` line;
  a change to `thunar.conf` must update the assertion.

## Modify this repo

- Edit the `thunar:` candy entity AND the `thunar-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a behaviour
  change not mirrored in the skill leaves the corpus stale.
- A change to the Sway binding belongs in `thunar.conf` and in the matching
  `check:` assertion, in the same change.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
