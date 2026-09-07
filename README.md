# homebrew-tui-do

A [Homebrew](https://brew.sh) tap for [tui-do](https://github.com/sjwasko/tui-do), a fast,
local-first terminal client for Vikunja.

```sh
brew tap sjwasko/tui-do
brew install tui-do
```

Or in one line, without tapping first:

```sh
brew install sjwasko/tui-do/tui-do
```

## What this builds

**From source, on purpose.** The formula compiles tui-do rather than downloading a
prebuilt binary, which takes a few minutes the first time: it fetches and builds the whole
dependency tree, and SQLite is compiled from source by `rusqlite`'s `bundled` feature.

**It is not free, and the original reason given for it was wrong.** On a clean Mac the
build dependencies are `llvm` (9,059 files, 1.6 GB) and `rust` (7,328 files, 432 MB), plus
`libgit2` — roughly 2 GB fetched to produce an 11 MB binary. `brew uninstall tui-do` does
not reclaim that; `brew autoremove` does.

This README used to justify the cost by saying a downloaded binary is quarantined by
Gatekeeper. **Measured on a Mac on 2026-09-07, that is not so**: a release asset fetched
with `curl` carries no extended attributes at all, because quarantine is set by the
downloading application opting into it. Browsers do; `curl` does not — which is also why
`brew install` of a bottled formula never prompts.

What is still true is smaller: a browser download *is* quarantined, and an arm64 binary
must be signed to run at all, though ad-hoc signing is enough and the Rust toolchain does
it while linking. A prebuilt macOS binary is therefore likely the better default, and this
tap will pour one once the release workflow builds it.

Homebrew installs the Xcode Command Line Tools it needs, so the C toolchain that
`bundled` SQLite requires is already handled.

## Linux

This works on Homebrew for Linux too, but there is little reason to use it: tui-do ships
**statically linked binaries** for `x86_64` and `aarch64` that need no Rust, no C
toolchain and no system SQLite. Take those from
[the releases page](https://github.com/sjwasko/tui-do/releases) instead.

## After installing

There is no first-run wizard and no config is written for you, so the first run stops with
`could not read …/config.yaml`. `brew info tui-do` repeats the setup, and the full version
is in [the main README](https://github.com/sjwasko/tui-do#required---first-time-setup).

Note that **macOS keeps these files somewhere other than the Linux examples**:

| | |
|---|---|
| config | `~/Library/Application Support/tui-do/config.yaml` |
| token | `~/Library/Application Support/tui-do/token` |
| store | `~/Library/Application Support/tui-do/tui-do.db` |

All three share one directory on macOS, where Linux splits config from data.

## Issues

**Report them on the main repository**, not here:
<https://github.com/sjwasko/tui-do/issues>. This tap is one formula file; anything that is
not a packaging problem belongs where the code is.

Note that the main repository is a **read-only mirror** of a private Forgejo instance, so
pull requests against it cannot be merged. Open an issue first. This tap is the exception:
it lives on GitHub natively, because a Homebrew tap has to.

## License

The formula is offered under the same terms as tui-do itself: MIT or Apache-2.0, at your
option.
