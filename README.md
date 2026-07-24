# @devolutions/iron-remote-desktop-rdp — aktraen build

**Built artifact**, not source. This is the WASM RDP backend for `@devolutions/iron-remote-desktop`,
rebuilt from the aktraen fork of IronRDP with a single behavioural patch:

- **`Config.autologon` is derived from credential presence** (`build_config` in
  `crates/ironrdp-web/src/session.rs`) instead of the upstream hardcoded `false`
  (upstream `TODO(#327)`). A browser client handed both a username and a password intends
  to log in; without `INFO_AUTOLOGON` xrdp shows its login dialog even with credentials
  supplied. Same semantics as FreeRDP (`/u` + `/p` implies autologon).

Source + patch: https://github.com/aktraen/IronRDP/tree/aktraen/autologon
Upstream: https://github.com/Devolutions/IronRDP (MIT OR Apache-2.0), published commit `e45f68c7`.

Consumed by `frontends/learn` for ADR-0083 trainee-desktop access. Rebuild: `wasm-pack build
--release --target web` in `crates/ironrdp-web`, then `npm run build-alone` in
`web-client/iron-remote-desktop-rdp`, then copy `dist/*` here.
