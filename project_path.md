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

:bangbang: Please check and remove
cargo tree --depth 1|sed -n '1!p'

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
>Rust force update / delete / re-installed all binary
><!-- keep the format -->
>- create scripts
><!-- To comply with the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
># show was is already installed
>cargo install --list
># create script for uninstall 
>cargo install --list |grep "^\s\s\s\s*" |xargs -n 1 echo "cargo uninstall " | tee /tmp/rust_uninstall_creates.sh
># create script for re-install 
>cargo install --list |grep "^\s\s\s\s*" |xargs -n 1 echo "cargo install " | tee /tmp/rust_install_creates.sh
># create script for install with sccache
>cargo install --list |grep "^\s\s\s\s*" |xargs -n 1 echo "time RUSTC_WRAPPER=sccache cargo install " | tee /tmp/rust_install_w_sccache_creates.sh
>```
><!-- keep the format -->
>- Check the scripts before you uses
>- :bangbang: TODO  use variable for cases, shebang
><!-- keep the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
>cat /tmp/rust_uninstall_creates.sh
>cat /tmp/rust_install_creates.sh
>cat /tmp/rust_install_w_sccache_creates.sh
>```
><!-- keep the format -->
>- Make scripts  executable
><!-- keep the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
>chmod +x /tmp/rust_uninstall_creates.sh
>chmod +x /tmp/rust_install_creates.sh
><chmod +x /tmp/rust_install_w_sccache_creates.sh
>```
><!-- keep the format -->
>- Generate first all script
><!-- keep the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
>```
><!-- keep the format -->
>- Run One of the two script for installing
><!-- keep the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
>/tmp/rust_install_creates.sh
>/tmp/rust_install_w_sccache_creates.sh
>```
><!-- keep the format -->
>- check again
><!-- keep the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
>cargo install --list
>```
><!-- keep the format -->
>- check again of filesystem level  too
><!-- keep the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
>ls -la ~/.cargo/bin
>```
<!-- keep the format -->
>[!TIP]
>Rust force update / delete / re-installed all creates
><!-- keep the format -->
>- Show which creates are already installed in current project
><!-- keep the format -->
>```bash <!-- markdownlint-disable-line code-block-style -->
>cargo tree --depth 1|sed -n '1!p' |awk '{print $2}'
>```
<!-- keep the format -->
>
<!-- keep the format -->
>[!NOTE]
>cargo list - like cargo install --list  
>With more information
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
>[!WARNING]  
> next point
> cargo tree
>echo "├── json v0.12.4"| cut -d ' ' -f 2
<!-- keep the format -->
>[!NOTE]
>cargo install --help  
>Install a Rust binary -- system wide  
><!-- markdownlint-disable MD033 -->
> Usage: cargo install [OPTIONS] [CRATE[@<VER>]]...
><!-- markdownlint-enable MD033 -->
>--list  List all installed packages and their versions
><!-- keep the format -->
>User folder for Rust binary
>**ls -la ~/.cargo/bin**
><!-- keep the format -->
<!-- keep the format -->
>[!NOTE]
>cargo add --help  
>Add dependencies to a **Cargo.toml** manifest file -- project scope
><!-- keep the format -->

>[!NOTE]
>cargo tree --help  
>Display a tree visualization of a dependency graph
>
>Used:
>**cargo tree --depth 1**
> "❌" OLD Please fix it  cut -d ' ' -f 2
>Get plain name dependency without version
>**cargo tree --depth 1|sed -n '1!p' |awk '{print $2}'**  
><!-- keep the format -->
<!-- keep the format -->
>"❌" The format should reviewed :grin:
>[!NOTE]
>cargo remove --help
>Remove dependencies from a project/**Cargo.toml** manifest file
>**cargo remove serde**
>
>Generate script for remove all installed crates from project
>"❌" Pls Add -> Shebang, return code. set -e. MISSING
>**cargo tree --depth 1|sed -n '1!p' |awk '{print $2}'|xargs -n 1 echo "cargo remove " >/tmp/rust_remove_dependencies.sh**
>
>Generate script for install crates to project
>>[!IMPORTANT] Before you run the remove script
>**cargo tree --depth 1|sed -n '1!p' |awk '{print $2}'|xargs -n 1 echo "cargo add " >/tmp/rust_add_dependencies.sh**
>
>- Make the script executable
>**chmod +x /tmp/rust_remove_dependencies.sh**
>**chmod +x /tmp/rust_add_dependencies.sh**
>- Check before you as used
>**cat /tmp/rust_remove_dependencies.sh**
>**cat /tmp/rust_add_dependencies.sh**
><!-- keep the format -->
<!-- keep the format -->
>[!NOTE]
>cargo add --help
>Add dependencies to a Cargo.toml manifest file
>Remove dependencies from a project/**Cargo.toml** manifest file - From cargo toml file
>**cargo remove serde**
><!-- keep the format -->
<!-- keep the format -->
>[!NOTE]
>cargo-modules [![alt text][1]]([./README.md](https://crates.io/crates/cargo-modules))
>A cargo plugin for visualizing/analyzing a crate's internal structure
><!-- keep the format -->
<!-- keep the format -->
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

## garbage garage
<!-- keep the format -->
>/tmp/rust_uninstall._creates.sh
><!-- keep the format -->
>- second method for generate script
><!-- keep the format -->
>- cargo install --list  |cut -d " " -f1 | grep -v "^$" |xargs -n 1 echo "cargo uninstall "
><!-- keep the format -->
>- Show which creates are installed now
>cargo install --list
>- re-install - preselect in generated file avoid for new install
>- make executable
>chmod +x /tmp/rust_install_creates.sh
><!-- keep the format -->
<!-- keep the format -->