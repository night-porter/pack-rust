# Night Porter pack: Rust

clippy, rustfmt and tests on every fix, plus review of `unsafe`, error handling, MSRV, public API and `Cargo.lock` changes.

A [Night Porter](https://night-porter.com) pack: prompts only, no code. Like every pack it can
only make Night Porter stricter: it adds instructions and read-only gates, and can't skip its
trust rules, checks or approvals.

```sh
nightporter market update
nightporter pack add rust
```

Then enable it in `[defaults]` or a repo file (`repos/<forge>/<owner>/<repo>.toml`):

```toml
packs = ["rust"]
```

| step | hook | what it does |
|---|---|---|
| `standards` | `pre_fix` | error-handling style, `// SAFETY:` comments, MSRV, no surprise dependencies or API changes |
| `check` | `post_fix` | `cargo fmt`, `cargo clippy --all-targets --locked -D warnings`, `cargo test --locked` |
| `review` | `pre_push` | blocks undocumented `unsafe` and weakened tests/lints; asks before dependency, MSRV, edition or public API changes |

Allow the cargo commands in your config (Claude Code only; Codex has no per-command list):

```toml
allow_commands = ["cargo fmt", "cargo clippy", "cargo test"]
```

Read every file before installing: they steer an agent that can edit your code. See
[Writing packs](https://docs.night-porter.com/writing-packs).

Licensed under either of Apache-2.0 or MIT, at your option.
