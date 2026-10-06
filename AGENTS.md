# Repository guidance

## Scope and local execution constraints

- This repository is the `nirier/diffr` fork of `mookid/diffr`. Planned work includes GitHub Releases and project changes.
- Do not run `cargo build` locally or install dependencies, tools, or Rust components locally.
- Do not run local commands that implicitly compile or fetch dependencies, including `cargo test`, `cargo run`, `cargo install`, and `cargo check`. Perform compilation and executable tests in CI.
- Use source inspection, diffs, and available tools that do not compile or install dependencies for local verification. Report which checks were performed and which require CI.

## Project structure

- `Cargo.toml` / `Cargo.lock`: Rust 2018 binary crate `diffr`; dependencies are `bstr` and `termcolor`.
- `src/main.rs`: stdin/stdout processing, unified diff parsing, highlighting, and application configuration.
- `src/cli_args.rs`: command-line parsing, colors, help, and version output.
- `src/diffr_lib/mod.rs` / `best_projection.rs`: tokenization and longest common subsequence algorithms.
- `src/tests_app.rs`, `src/tests_cli.rs`, and `src/diffr_lib/tests_lib.rs`: existing tests. CLI tests require a built binary; CI currently builds before testing.
- `assets/h.txt`, `assets/help.txt`, and `assets/diffr.1.md`: short help, long help, and manual source. Keep relevant documentation consistent with CLI changes.
- `README.md` and `CHANGELOG.md`: user documentation and release history.
- `azure-pipelines.yml` / `ci/`: existing Azure CI for Linux, macOS, and Windows.
- `.github/workflows/release.yml`: tag-triggered GitHub Releases with tested Linux x86_64 glibc and musl archives and checksums.

## Changes and releases

- Keep edits focused on the requested behavior and follow the existing Rust style.
- Preserve upstream attribution and license. Distinguish fork releases from upstream packages and distribution instructions.
- When adding GitHub release automation, run builds and dependency setup on hosted CI runners. Use explicit targets and archive names, include license/documentation where appropriate, and grant only the permissions each job needs.
- Keep release tags and the crate version consistent. Do not publish to crates.io unless explicitly requested.
- Do not push tags, publish releases, or otherwise trigger publication unless the user requests it. Preparing workflow files is allowed as part of release automation work.
- Add or update meaningful regression tests for behavior changes, and execute them in CI under the local execution constraints above.
- Communicate with the user in Chinese unless requested otherwise.
