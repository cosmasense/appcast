# Cosma Sense Appcast

Public Sparkle update feeds for the Cosma Sense macOS app. Hosted via
GitHub Pages at:

- Stable: <https://cosmasense.github.io/appcast/stable.xml>
- Dev:    <https://cosmasense.github.io/appcast/dev.xml>

## Don't edit by hand

Both XML files are appended to by `release/scripts/publish.sh` in the
[fileSearchForntend](https://github.com/EthanPany/fileSearchForntend)
repo. The script signs each release with the EdDSA private key in the
maintainer's keychain (matching the `SUPublicEDKey` baked into shipped
app bundles), so any hand-written entry would simply be rejected by
clients.

## Why a separate repo

The appcast URL is a permanent contract — every installed app polls
it forever. Keeping it in its own repo means we can rotate the
frontend repo / branch / hosting strategy without orphaning installed
clients. As long as <https://cosmasense.github.io/appcast/> keeps
serving the same XML, every existing app stays on the upgrade path.

## Channel semantics

- `stable.xml` — public releases. Tagged `v1.2.3` on the frontend
  repo. Default channel for new installs.
- `dev.xml`    — prereleases. Tagged `v1.2.3-dev` and marked as
  prereleases on GitHub. Users opt in via
  Settings → General → App Updates → Release Channel.
