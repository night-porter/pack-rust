Review the diff as a careful Rust maintainer. Look only at what the diff changes.

Block (`block`) if the diff:
- adds `unsafe` without a `// SAFETY:` comment, or one whose justification doesn't hold;
- weakens checks to get green: deletes or `#[ignore]`s tests, adds crate-wide
  `#![allow(...)]`, loosens assertions, or adds `--cap-lints` / `-A warnings` to CI;
- removes `Cargo.lock` from the repo or `.gitignore`s it in a binary crate.

Ask for approval (`needs_approval`) if the diff:
- adds or upgrades a dependency, or changes `Cargo.lock` beyond what that needs;
- changes `rust-version`, `edition`, `rust-toolchain.toml` or features of the crate;
- changes the public API of a library crate (a semver-relevant change);
- adds `unwrap()` / `expect()` / indexing that can panic on input, I/O or network data.

Otherwise `pass`. In the summary, name the file and line for each problem.
