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

That is slower than pouring a bottle and it is the right trade on macOS today. A binary
downloaded over the network carries the `com.apple.quarantine` attribute, so Gatekeeper
refuses to run it with *"the developer cannot be verified"* unless it has been signed and
notarised with a paid Apple Developer account. Something built locally never acquires the
attribute, so the problem does not arise rather than being worked around.

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
