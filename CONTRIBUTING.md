# Contributing to Vloom Audio

Thanks for helping! This guide applies to every repository in the
[vloom-audio](https://github.com/vloom-audio) organisation.

## Ways to help

- **Report a bug**: open an issue with steps to reproduce, your OS and audio device.
- **Suggest a feature**: open an issue describing the problem it solves, not only the solution.
- **Fix something**: look for issues labelled `good first issue` or `help wanted`.
- **Test builds** on your machine and tell us what breaks.

Please search existing issues first so we keep each topic in one place.

## Before a large change

Open an issue (or comment on an existing one) before starting big work such as
a new feature, a refactor or a new dependency. A short discussion up front saves
everyone from a pull request that cannot be merged.

## Development setup

```sh
mkdir vloom-audio && cd vloom-audio
git clone https://github.com/vloom-audio/VloomDAW.git
VloomDAW/scripts/bootstrap.sh       # clones vloom-engine next to it
```

Every repository builds the same way with CMake presets:

```sh
cmake --preset dev && cmake --build --preset dev && ctest --preset dev
```

Full setup per OS is in each repository's `docs/getting-started.md`. Read
`docs/architecture.md` before your first change: it says where code goes.

| Repository | What lives there |
|---|---|
| [vloom-engine](https://github.com/vloom-audio/vloom-engine) | Everything that touches audio samples, timing or devices |
| [VloomDAW](https://github.com/vloom-audio/VloomDAW) | The Qt app: windows, widgets, project model, undo |
| [.github](https://github.com/vloom-audio/.github) | Org profile and these shared guidelines |

## Pull requests

1. Fork, then branch from `main` (`fix/metronome-drift`, `feat/step-sequencer`).
2. Keep each pull request to one topic. Small PRs get reviewed faster.
3. Add or update tests when you change engine behaviour or app logic in `core/`.
4. Run `scripts/format.sh` before committing.
5. Add a line to `CHANGELOG.md` under *Unreleased* for user-visible changes.
6. Make sure CI passes on all three platforms.

### Commit messages

We use [Conventional Commits](https://www.conventionalcommits.org/):

```
feat(engine): add swing to the step sequencer
fix(ui): keep playhead label from flickering
docs: explain the render graph
```

Types: `feat`, `fix`, `perf`, `refactor`, `test`, `docs`, `build`, `ci`, `chore`.

## Code rules that matter most

- **The audio thread is sacred.** Code reached from `Engine::process()` must not
  allocate, lock, wait, log or touch files. If in doubt, ask in the PR.
- Follow the existing style (`.clang-format`, `.editorconfig`).
- Prefer clear code over clever code. Comment the *why*, not the *what*.

## Licensing of contributions

All Vloom Audio code is licensed under **GPL-3.0-or-later**. By submitting a
pull request you agree that your contribution is licensed under the same
terms. Only submit code you wrote yourself or that is GPL-compatible, and keep
the original copyright notice on anything you bring in.

## Conduct

Everyone taking part must follow our [Code of Conduct](CODE_OF_CONDUCT.md).
