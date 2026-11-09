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

## What this installs

**The prebuilt Apple Silicon binary from the tui-do release**, checked against the
release's SHA-256. Nothing is compiled, so nothing else is installed: no Rust, no LLVM, no
C toolchain. Until v1.1.0 this tap built from source, which fetched about 2 GB of build
tools to produce an 11 MB binary. If you installed it that way, `brew autoremove` gives that
space back.

**Apple Silicon only**, the same as the release. On an Intel Mac,
[build from source](https://github.com/sjwasko/tui-do#building-from-source).

Gatekeeper does not get involved. Quarantine is set by the program that downloads a file,
and browsers set it while `curl` and Homebrew do not. The binary is ad-hoc signed, which is
all an arm64 binary needs to run.

## Linux

Not offered here. tui-do ships **statically linked binaries** for `x86_64` and `aarch64`
Linux that need no Rust, no C toolchain and no system SQLite. Take those from
[the releases page](https://github.com/sjwasko/tui-do/releases).

## After installing

```sh
tui-do login
```

It asks for your server, opens Vikunja's API-token page, checks the token you paste, and
writes the config. On macOS the files live together in one directory, not where the main
README's Linux examples put them:

| | |
|---|---|
| config | `~/Library/Application Support/tui-do/config.yaml` |
| token | `~/Library/Application Support/tui-do/token` |
| store | `~/Library/Application Support/tui-do/tui-do.db` |

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
