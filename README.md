# Develop

## Prerequisites

```bash
cargo install dioxus-cli
rustup target add wasm32-unknown-unknown
```

## How to build

```bash
dx build --release
```

## Run

```bash
dx serve --hot-reload --platform desktop
```

# Issues

```shell-session
$ dx build --release                                                                                                                                                                        22:13:01
[WARN] You appear to be creating a Dioxus project from scratch; we will use the default config
[INFO] 🚅 Running build command...
Error: 🚫 Building project failed: error: Only features sync,macros,io-util,rt,time are supported on wasm.
   --> /home/neonew/.cargo/registry/src/index.crates.io-6f17d22bba15001f/tokio-1.35.1/src/lib.rs:471:1
    |
471 | compile_error!("Only features sync,macros,io-util,rt,time are supported on wasm.");
    | ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

error: could not compile `tokio` (lib) due to 2 previous errors
```

I've tried to specify the features via `cargo add tokio --features sync,macros,io-util,rt,time`, but that
didn't fix it.

Interestingly, `cargo build --release` worked without error. Hmm.

# Thoughts on Dioxus

- Uses it's own cli tool `dx`, instead of using the default cargo build process. I dislike this.
- Small footprint for a HTML/CSS GUI solution, uses the WebView of the system. Good.
  This is similar to Tauri (which essentially is used under the hood if I understood correctly),
  which I have tested [in the past](https://andreas-mausch.de/blog/2020-02-20-tauri/).
- The code can be re-used for all supported platforms, including mobile and web. Very nice.
