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
>Creates force update / delete / re-installed all crates
<!-- To comply with the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
# show was is already installed
cargo install --list
# create script for uninstall 
cargo install --list |grep "^\s\s\s\s*" |xargs -n 1 echo "cargo uninstall " >/tmp/rust_uninstall_creates.sh
# create script for re-install 
cargo install --list |grep "^\s\s\s\s*" |xargs -n 1 echo "cargo install " >/tmp/rust_install_creates.sh
# create script for re-install with sccache
cargo install --list |grep "^\s\s\s\s*" |xargs -n 1 echo "time RUSTC_WRAPPER=sccache cargo install " >/tmp/rust_install_w_sccache_creates.sh
# make executable
chmod +x /tmp/rust_uninstall._creates.sh 
# run the script for uninstalled
/tmp/rust_uninstall._creates.sh
# second method for generate script
# cargo install --list  |cut -d " " -f1 | grep -v "^$" |xargs -n 1 echo "cargo uninstall "
# Show which creates are installed now
cargo install --list
# re-install - preselect in generated file avoid for new install
# make executable
chmod +x /tmp/rust_install_creates.sh
# run the script for installed
/tmp/rust_install_creates.sh

```
<!-- To comply with the format -->
>[!NOTE]
>cargo install --help  
>Install a Rust binary -- system wide  
>
><!-- markdownlint-disable MD033 -->
> Usage: cargo install [OPTIONS] [CRATE[@<VER>]]...
><!-- markdownlint-enable MD033 -->
> --list                     List all installed packages and their versions
><!-- keep the format -->
>folder for Rust binary
>**ls -la ~/.cargo/bin**
><!-- keep the format -->
<!-- keep the format -->
>[!NOTE]
>cargo add --help
>Add dependencies to a **Cargo.toml** manifest file -- project scope
><!-- keep the format -->
<!-- keep the format -->
>[!NOTE]
>cargo list - same output cargo install --list but with more information
>List and update installed crates
>**cargo install cargo-list**
>
>used
>**cargo list**
><!-- markdownlint-disable MD058 -->
>|  # | Name        | Pinned | Installed | Available |
>|---:|-------------|--------|-----------|-----------|
>|  1 | cargo-cache |        | 0.8.3     |           |
>|  2 | cargo-list  |        | 0.32.0    |           |
><!-- markdownlint-enable MD058 -->
><!-- keep the format -->
<!-- keep the format -->
>[!NOTE]
>cargo tree --help
>Display a tree visualization of a dependency graph
>
>**cargo tree --depth 1**

[!NOTE] For later
cargo tree --depth 1
cargo-modules https://crates.io/crates/cargo-modules

##########
cargo add --help
Add dependencies to a Cargo.toml manifest file

<!-- keep the format -->
>[!NOTE]
>Symbol to mark web external links [![alt text][1]](./README.md)
<!-- make folder and download the link sign vai curl -->
<!-- mkdir -p img && curl --create-dirs --output-dir img -O  "https://raw.githubusercontent.com/MathiasStadler/link_symbol_svg/refs/heads/main/link_symbol.svg"-->
<!-- Link sign - Don't Found a better way :-( - You know a better method? - send me a email -->
[1]: ./img/link_symbol.svg
