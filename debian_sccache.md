# debian sccache
<!-- keep the format -->
- [Sccache](#Sccache - Shared Compilation Cache)
- [Os](os)
- [Installation](#installation)
- [Usage](#usage)

## Sccache - Shared Compilation Cache [![alt text][1]](https://github.com/mozilla/sccache/tree/main)
<!-- keep the format -->
<!-- spell-checker: disable  -->
- Sccache - **S**hared **C**ompilation **Cache**
<!-- spell-checker: enable-->
- sccache is a ccache [![alt text][1]](https://ccache.dev) like compiler caching tool
- It is used as a compiler wrapper and avoids compilation when possible
- storing cached results either on local disk
-- or in one of several cloud storage backends
- speedup Rust builds
- save deployments time
<!-- keep the format -->
## OS-Version
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
$ uname -a
Linux debian 6.1.0-28-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.119-1 (2024-11-22) x86_64 GNU/Linux
```
<!-- keep the format -->
## Hardware
<!-- keep the format -->
:bangbang: Data missing
<!-- keep the format -->
## Installation
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
sudo apt update
sudo apt install sccache
if [ $? == 0 ]; then echo -e "command return code $? => Ok ";else echo "Error $? => Error"; fi;
```
<!-- keep the format -->
## Version of sccache - sccache 0.10.0
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
sccache --version
#sccache 0.10.0
if [ $? == 0 ]; then echo -e "command return code $? => Ok ";else echo "Error $? => Error"; fi;
```
<!-- keep the format -->
## Setup for user
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
cd #change to home folder
mkdir -p .cargo #-p, --parents     no error if existing ...
cat > .cargo/config.toml << 'EOF'
# FOUND HERE
# https://markaicode.com/rust-compiler-performance-2025/
# path of sccache binary
# which sccache
[build]
jobs = 4                # Set to your CPU core count
rustc-wrapper = "/usr/bin/sccache"
#rustc-wrapper = "sccache" # Enables disk caching
#pipelining = true        # Enables build pipelining
#This option is deprecated and unused. Cargo always has pipelining enabled
# SEE HERE https://doc.rust-lang.org/cargo/reference/config.html

[profile.dev]
incremental = true       # Enable incremental compilation
codegen-units = 4       # Enables parallel code generation, one per available core
EOF
```

## Incremental compilation in detail [![alt text][1]](https://rustc-dev-guide.rust-lang.org/queries/incremental-compilation-in-detail.html)

## incremental = true [![alt text][1]](https://doc.rust-lang.org/cargo/reference/profiles.html#incremental)
<!-- keep the format -->
The incremental setting controls the -C incremental flag which controls whether or not incremental compilation is enabled. Incremental compilation causes rustc to save additional information to disk which will be reused when recompiling the crate, improving re-compile times. The additional information is stored in the target directory.

The valid options are:

true: enabled
false: disabled
Incremental compilation is only used for workspace members and “path” dependencies.

The incremental value can be overridden globally with the CARGO_INCREMENTAL environment variable or the build.incremental config variable.

## codegen-units [![alt text][1]](https://doc.rust-lang.org/cargo/reference/profiles.html#codegen-units)

The codegen-units setting controls the -C codegen-units flag which controls how many “code generation units” a crate will be split into. More code generation units allows more of a crate to be processed in parallel possibly reducing compile time, but may produce slower code.

This option takes an integer greater than 0.

The default is 256 for incremental builds, and 16 for non-incremental builds.

<!-- keep the format -->
## Status/start/stop of sccache [![alt text][1]](https://linuxcommandlibrary.com/man/sccache)
<!-- keep the format -->
sccache --show-stats
sccache --show-adv-stats
sccache --zero-stats
sccache --start-server
sccache --stop-server

## Another useful parameter [![alt text][1]](https://linuxcommandlibrary.com/man/sccache)

PARAMETERS

<!--markdownlint-disable -->
<!--markdownlint-enable -->

Options:
  -s, --show-stats                     show cache statistics
      --show-adv-stats                 show advanced cache statistics
      --start-server                   start background server
      --debug-preprocessor-cache       show all preprocessor cache entries
      --stop-server                    stop background server
  -z, --zero-stats                     zero statistics counters
      --dist-auth                      authenticate for distributed compilation
      --dist-status                    show status of the distributed client
<!--markdownlint-disable -->
      --package-toolchain <EXE> <OUT>  package toolchain for distributed compilation
      --stats-format <FMT>             set output format of statistics [default: text] [possible values: text, json]
<!--markdownlint-enable -->
  -h, --help                           Print help
  -V, --version                        Print version

## try out [![alt text][1]](https://android.googlesource.com/platform/prebuilts/android-emulator-build/common/+/emu-master-dev/sccache/linux-x86_64/README.md)
<!-- keep the format -->
SCCACHE_ERROR_LOG=/tmp/sccache_log.txt SCCACHE_LOG=debug sccache
<!-- keep the format -->
## Clear cache
<!-- keep the format -->
- Find the path of cache
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
sccache --show-stats |grep location
```
<!-- keep the format -->
- Current size of cache
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
du -h ~/.cache/sccache
```
<!-- keep the format -->
- stop. delete folder content start sccache
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
sccache --stop-server
# process really terminate :-)
ps -ef|grep sccache | grep -v grep
# delete folder content
rm -rfv ~/.cache/sccache/*
# start sccache
sccache --start-server
# check process
ps -ef|grep sccache | grep -v grep
# show activity
sccache --show-stats
```

## rust project compile with sccache [![alt text][1]](https://earthly.dev/blog/rust-sccache/)
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
```
<!-- keep the format -->
## Create local config file [![alt text][1]](https://deepwiki.com/mozilla/sccache/2.1-configuration)
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
mkdir -p  ~/.config/sccache
touch ~/.config/sccache/config
cat > ~/.config/sccache/config << 'EOF'
# Server configuration options
server_startup_timeout_ms = 10000

# Cache configuration sections 
[cache.disk]
# dir = "/path/to/cache"
dir = "/home/trapapa/.cache/sccache"
size = 10737418240  # 10 GiB
rw_mode = "READ_WRITE"  # or "READ_ONLY"

[cache.disk.preprocessor_cache_mode]
use_preprocessor_cache_mode = true
file_stat_matches = false
use_ctime_for_stat = true
ignore_time_macros = false
skip_system_headers = false
hash_working_directory = true

EOF
```
<!-- keep the format -->
| Column 1      | Column 2      |
| ------------- | ------------- |
| Cell 1, Row 1 | Cell 2, Row 1 |
| Cell 1, Row 2 | Cell 1, Row 2 |
<!-- keep the format -->
<!-- keep the format -->
<!-- markdownlint-disable -->
| Option                      |Description                                            | Default |   
| ----------------------------|-------------------------------------------------------| ------- |
| use_preprocessor_cache_mode | Enable/disable preprocessor cache mode                | true    |
| file_stat_matches           | Compare header files by size/time rather than content | false   |
| use_ctime_for_stat          | Use ctime to check file changes                       | true    |
| ignore_time_macros          | Ignore time macros (_DATE_,_TIME_,_TIMESTAMP__)       | false   |
| skip_system_headers         | Don't cache system headers, only add them to the hash | false   |
| hash_working_directory      | Include working directory in the hash                 | true    |
<!-- markdownlint-enable -->
<!-- keep the format -->
## Usage with RUST based projects
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
time cargo new sccache_base_project
Creating binary (application) `sccache_base_project` package
note: see more `Cargo.toml` keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

real 0m0.134s
user 0m0.087s
sys 0m0.044s

# change into project folder
cd sccache_base_project

# run cargo build with sccache log

```

SCCACHE_ERROR_LOG=/tmp/sccache_log.txt SCCACHE_LOG=debug sccache cargo build

- build

## Usage
<!-- keep the format -->
```bash <!-- markdownlint-disable-line code-block-style -->
export RUSTC_WRAPPER=sccache
cargo build
```
<!-- keep the format -->
<!-- keep the format -->
>[!NOTE]
>Symbol to mark web external links [![alt text][1]](./README.md)
<!-- make folder and download the link sign vai curl -->
<!-- mkdir -p img && curl --create-dirs --output-dir img -O  "https://raw.githubusercontent.com/MathiasStadler/link_symbol_svg/refs/heads/main/link_symbol.svg"-->

<!-- Link sign - Don't Found a better way :-( - -->
<!-- You know a better method? - send me a email -->

[1]: ./img/link_symbol.svg
<!-- Avoid MD047/single-trailing-newline: -->
<!-- Files should end with a single newline character -->