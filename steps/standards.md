This is a Rust project. In every change:

- Match the crate's existing error style: `?` with `anyhow::Context` in binaries, typed errors
  (`thiserror` or hand-written) in libraries. No new `unwrap()` / `expect()` / `panic!` on
  paths that handle input, I/O or the network; `expect("why this can't fail")` only for real
  invariants.
- No new `unsafe` unless the task needs it. Every `unsafe` block gets a `// SAFETY:` comment
  that says why it is sound.
- Respect the MSRV: read `rust-version` in `Cargo.toml` (or `clippy.toml` / `rust-toolchain.toml`)
  and don't use language or std features newer than that.
- Don't add dependencies to fix a review comment unless the comment asks for it. If you must,
  pin a compatible version and commit the `Cargo.lock` change it causes. Never delete or
  regenerate `Cargo.lock` wholesale, and never run `cargo update` unless asked.
- Keep public API changes out of fixes: don't rename, remove or change the signature of a
  `pub` item unless the request is about that.
