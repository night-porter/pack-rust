Before you finish, run on the workspace (add `--all-features` if the CI config does):

1. `cargo fmt --all`. Keep the formatting of files you changed; revert it in files you didn't
   otherwise touch, so the fix stays reviewable.
2. `cargo clippy --all-targets --locked -- -D warnings` and fix the warnings in code you touched.
   Don't add `#[allow(...)]` to silence them unless the lint is wrong for that line, and then
   say why in a comment.
3. `cargo test --locked` (or the test command in CI). If a test fails that you didn't touch and
   it also fails on the base commit, say so in your summary instead of changing the test.

If `--locked` fails because the lock file is out of date, report it; don't run `cargo update`.
If a command can't run (no network for new crates, sandbox), say which and why.
