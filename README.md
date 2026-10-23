# Warp Terminal-Only (macOS)

A macOS-only build of the Warp terminal with the AI, agent, cloud, account, session-sharing, code-review, and team features removed from the user-facing app.

This is based on the open-source Warp client. The goal is a focused terminal application:

- Local terminal sessions and blocks
- Bottom-pinned input
- Split panes and tabs
- File explorer and folder/path completion
- Markdown/file viewer
- Themes, appearance, and keybinding settings
- Local workflows
- Command search and history

The app is configured to fail closed for network access: Warp/Firebase/Oz endpoints point at unreachable loopback addresses, and the only listening socket is the local terminal server.

## Build requirements

- macOS with Xcode Command Line Tools
- Rust `1.92.0` (installed automatically via `rust-toolchain.toml` when using `rustup`)
- `cargo-bundle`
- `jq`

```bash
xcode-select --install
cargo install cargo-bundle
brew install jq
```

## Build and run

From the repository root:

```bash
WARP_SKIP_COMMON_SKILLS_INSTALL=1 \
WARP_BIN_NAME=warp-oss \
WARP_CHANNEL=oss \
FEATURES="skip_login" \
./script/macos/run
```

To build without launching:

```bash
WARP_SKIP_COMMON_SKILLS_INSTALL=1 \
WARP_BIN_NAME=warp-oss \
WARP_CHANNEL=oss \
FEATURES="skip_login" \
./script/macos/run --dont-open
```

The app bundle is written to:

```text
target/debug/bundle/osx/WarpOss.app
```

Open it with:

```bash
open -n target/debug/bundle/osx/WarpOss.app
```

The bundle is ad-hoc signed for local development. On another Mac, macOS may require right-clicking the app and choosing **Open** the first time.

## Repository layout

- `app/` — macOS application
- `crates/` — supporting Rust crates
- `script/` — build and run scripts
- `target/` — local build output (ignored by git)

## License

Warp's UI framework (`warpui_core` and `warpui`) is MIT licensed. The rest of the source is AGPL-3.0. See `LICENSE-MIT`, `LICENSE-AGPL`, and the upstream project for details.
