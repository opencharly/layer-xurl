# layer-xurl

The [xurl](https://github.com/xdevplatform/xurl) X (Twitter) API CLI for
OpenCharly images.

The `xurl` candy installs the `@xdevplatform/xurl` npm package globally (npm `-g`
into `~/.npm-global/bin`, placed on PATH by the nodejs layer). The package's
postinstall downloads the real platform binary, but npm ≥12 blocks install
scripts unless they are explicitly allowed, so the plan runs that one audited
download script itself after the global install.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `xurl` |
| Binary | `~/.npm-global/bin/xurl` |
| Requires | `layer-nodejs` |
| Install files | `charly.yml`, `package.json` |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list:

```yaml
my-social-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-xurl:v2026.243.0508'
```

Then, inside the built image:

```bash
xurl --help                       # usage
xurl /2/tweets -d '{"text":"..."}'   # post, search, DM, or fetch media
```

The candy's `plan:` runs the package's own `install.js` to fetch the platform
binary, then asserts the `xurl` CLI in the npm global bin and that it runs
`--help`.

## Layout

- `charly.yml` — the `xurl:` candy entity (the `require:` on `layer-nodejs`, the
  postinstall `run:` step, the `check:` assertions) and the embedded
  `xurl-skill:` skill entity.
- `package.json` — pins the `@xdevplatform/xurl` npm package.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:xurl`
- `/charly-coder:nodejs` — runtime dependency
- `/charly-hermes:hermes` — companion social/messaging agent
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
