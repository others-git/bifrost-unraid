# bifrost-unraid

Unraid [Community Applications](https://forums.unraid.net/topic/38582-plug-in-community-applications/)
template for **[Bifrost](https://github.com/others-git/bifrost)** — a self-hosted smart home control hub.

Bifrost bridges lights (Philips Hue, Govee, LIFX), audio (Sonos, Onkyo / Integra), and any
Home Assistant integration behind one fast web UI and REST API. It ships as a single static
binary with a single SQLite file, and runs from the published image
`ghcr.io/others-git/bifrost:latest`.

## Install on Unraid

1. In Unraid, go to the **Apps** tab (Community Applications) and search for **Bifrost**.
2. On the template:
   - Set a **Secret Key** (`BIFROST_SECRET`) — generate one with `openssl rand -hex 32`.
     This encrypts provider credentials at rest; changing it later orphans stored credentials.
   - Leave **Data Directory** at `/mnt/user/appdata/bifrost/data` (holds `bifrost.db`).
   - Leave **Bind Address** at `0.0.0.0:3000` unless you want a different port.
3. Apply. Bifrost runs on the **host network** — required so device auto-detect
   (SSDP/eISCP broadcast, multicast, subnet sweep) reaches your LAN.
4. Open `http://[server-ip]:3000/`. Pair Hue via the bridge link button in the UI.

## Repository layout

| Path | Purpose |
|---|---|
| `ca_profile.xml` | Repository overview/metadata shown in Community Apps. Must stay in the repo root. |
| `templates/bifrost.xml` | The Bifrost Docker app template. `TemplateURL` points at this file's raw URL. |
| `LICENSE` | MIT license. |

## Adding this repository manually

If it is not yet indexed by Community Applications, add the repo directly:
Community Applications → **Settings** → add this repository's URL.

The template's `TemplateURL` is pinned to:
`https://raw.githubusercontent.com/others-git/bifrost-unraid/main/templates/bifrost.xml`

## Updating

The template tracks the `:latest` image tag. New Bifrost releases are published to
`ghcr.io/others-git/bifrost` — Unraid's **Check for Updates** will pick them up.

## See also

- Bifrost source, API docs, and architecture: https://github.com/others-git/bifrost
- Unraid CA template reference: https://github.com/unraid/unraid-community-apps-starter
