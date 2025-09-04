# cargo-chef [![alt text][1]](https://crates.io/crates/cargo-chef)
<!-- keep the format -->
-A cargo sub-command to build project dependencies for optimal Docker layer caching
<!-- keep the format -->
- [Sccache](#Sccache - Shared Compilation Cache)
- [Another sources]
- [Os](os)
- [Install](#install)
- [Usage](#usage)
<!-- keep the format -->
## Another sources
<!-- keep the format -->
- lpalmieri.com - fast-rust-docker-builds [![alt text][1]](https://www.lpalmieri.com/posts/fast-rust-docker-builds/)
<!-- keep the format -->
## Install
<!-- keep the format -->
cargo install cargo-chef
<!-- keep the format -->
## command help output
<!-- keep the format -->
<!-- markdownlint-disable MD033 -->
Usage: cargo chef <COMMAND>
<!-- markdownlint-enable MD033 -->
Commands:
  prepare  Analyze the current project to determine the minimum subset of files (Cargo.lock and Cargo.toml manifests) required to build it and cache dependencies
  cook     Re-hydrate the minimum project skeleton identified by `cargo chef prepare` and build it to cache dependencies
  help     Print this message or the help of the given subcommand(s)
<!-- keep the format -->
Options:
  -h, --help     Print help
  -V, --version  Print version
<!-- keep the format -->
## Usage
<!-- keep the format -->
## Prepare examines your project and builds a recipe that captures the set of information required to build your dependencies
<!-- keep the format -->
cargo chef prepare --recipe-path recipe.json
<!-- keep the format -->
## Cook the project
<!-- keep the format -->
cargo chef cook --recipe-path recipe.json
>[!NOTE]
>Symbol to mark web external links [![alt text][1]](./README.md)
<!-- make folder and download the link sign vai curl -->
<!-- mkdir -p img && curl --create-dirs --output-dir img -O  "https://raw.githubusercontent.com/MathiasStadler/link_symbol_svg/refs/heads/main/link_symbol.svg"-->

<!-- Link sign - Don't Found a better way :-( - -->
<!-- You know a better method? - send me a email -->
[1]: ./img/link_symbol.svg
<!-- Avoid MD047/single-trailing-newline: -->
<!-- Files should end with a single newline character -->