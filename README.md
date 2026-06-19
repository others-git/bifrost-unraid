# bifrost-unraid

Unraid [Community Applications](https://forums.unraid.net/topic/38582-plug-in-community-applications/)
template for **[Bifrost](https://github.com/others-git/bifrost)** — a self-hosted smart home control hub.

Bifrost brings your lights (Philips Hue, Govee, LIFX), audio (Sonos, Onkyo / Integra),
power devices, and TVs/streamers under one web UI and REST API, and can also surface any
Home Assistant integration as a Bifrost device. It ships as a single binary with one
SQLite file, and runs from the published image `ghcr.io/others-git/bifrost:latest`.

**[➜ Install from Community Applications](https://ca.unraid.net/apps/bifrost-0ehyi200nwfgp8)** — or
search **Bifrost** on the Apps tab in Unraid.

## Install on Unraid

1. In Unraid, go to the **Apps** tab (Community Applications) and search for **Bifrost**.
2. On the template:
   - Set a **Secret Key** (`BIFROST_SECRET`) — generate one with `openssl rand -hex 32`.
     This encrypts provider credentials at rest; changing it later orphans stored credentials.
   - Leave **Data Directory** at `/mnt/user/appdata/bifrost/data` (holds `bifrost.db`).
   - Leave **Bind Address** at `0.0.0.0:3000` unless you want a different port.
3. Apply. Bifrost runs on the **host network** — required so device auto-detect
   (SSDP/eISCP broadcast, multicast, subnet sweep) reaches your LAN.
4. Open `http://[server-ip]:3000/`. Set the hub password on first load, then add
   providers. Pair Hue via the bridge link button in the UI.

Bifrost is built for a trusted LAN — one hub password, no per-user accounts. For
remote access, put it behind Tailscale, a VPN, or a TLS reverse proxy rather than
forwarding port 3000 to the internet.

## Repository layout

| Path | Purpose |
|---|---|
| `ca_profile.xml` | Repository overview/metadata shown in Community Apps. Must stay in the repo root. |
| `templates/bifrost.xml` | The Bifrost Docker app template. `TemplateURL` points at this file's raw URL. |
| `LICENSE` | MIT license. |

## Adding this repository manually

Bifrost is indexed in Community Applications (search **Bifrost**), so this is
rarely needed. To pull the template directly anyway — e.g. to test an unreleased
change — add the repo under Community Applications → **Settings**.

The template's `TemplateURL` is pinned to:
`https://raw.githubusercontent.com/others-git/bifrost-unraid/main/templates/bifrost.xml`

## Updating

The template tracks the `:latest` image tag. New Bifrost releases are published to
`ghcr.io/others-git/bifrost` — Unraid's **Check for Updates** will pick them up.

## See also

- Bifrost source, API docs, and architecture: https://github.com/others-git/bifrost
- Unraid CA template reference: https://github.com/unraid/unraid-community-apps-starter
