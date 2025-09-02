# project path of rust_improve_build_time_debian
<!-- To comply with the format -->
## Create for your own project a project folder in the Linux console (terminal ,bash shell), e.g. in your your own home directory, and then open this folder as a new project in the MS VSCODE program
<!-- To comply with the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
# cd && mkdir <project_name folder> && cd $_
# command 'cd' change to home folder from logged in user
cd && mkdir rust_improve_build_time_debian && cd $_
```
<!-- To comply with the format -->
## Init a new rust based project inside the previously generated folder
<!-- To comply with the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
touch README.md \
&& ln -s README.md README \
&& cargo init "." \
&& cargo add rustfmt \
&& rustup component add rustfmt \
&& mkdir examples \
&& cp src/main.rs examples/example.rs \
&& sed -i -e 's/world/example/g' examples/example.rs \
&& rustup  show \
&& rustup  check \
&& rustup toolchain uninstall stable \
&& rustup toolchain install stable \
&& rustup override set stable \
&& rustup update  --force \
&& rustup show \
&& mkdir tests \

```

## Install cargo cache [![alt text][1]](https://crates.io/crates/cargo-cache)
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cargo install cargo-cache
```
<!-- keep the format -->
## Show cargo cache
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cargo cache
```
<!-- keep the format -->
time RUSTC_WRAPPER=sccache cargo build

<!-- keep the format -->
## Show which toolchain is active
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
rustup show
# or better
rustup show |sed -n '/active toolchain/,/^$/p'
```
<!-- keep the format -->
## Switch between Rust toolchains  [![alt text][1]](https://stackoverflow.com/questions/58226545/how-to-switch-between-rust-toolchains)
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
rustup override set nightly
rustup override set stable
# another toolchain
rustup override set 1.85.0-x86_64-unknown-linux-gnu
```
<!-- keep the format -->
>[!TIP]
>Delete all installed crates
<!-- To comply with the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cargo install --list |grep "^\s\s\s\s*" |xargs -n 1 echo "cargo uninstall " >/tmp/uninstall.txt
cargo install --list  |cut -d " " -f1 | grep -v "^$" |xargs -n 1 echo "cargo uninstall "
cargo install --list
```
<!-- To comply with the format -->
<!-- keep the format -->
>[!NOTE]
>Symbol to mark web external links [![alt text][1]](./README.md)
<!-- make folder and download the link sign vai curl -->
<!-- mkdir -p img && curl --create-dirs --output-dir img -O  "https://raw.githubusercontent.com/MathiasStadler/link_symbol_svg/refs/heads/main/link_symbol.svg"-->
<!-- Link sign - Don't Found a better way :-( - You know a better method? - send me a email -->
[1]: ./img/link_symbol.svg
