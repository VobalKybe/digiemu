# Building the macOS app

The repository can build a real native `DigiEmu.app` on GitHub Actions. No Python installation is required on the user's Mac when using the generated ZIP.

## GitHub Actions

The workflow is `.github/workflows/macos-release.yml`.

### Manual build

Open **Actions → macOS app release → Run workflow**, enter the version (for example `0.2.0`), and run it. The workflow builds both:

- `DigiEmu-macOS-arm64.zip` for Apple Silicon
- `DigiEmu-macOS-x86_64.zip` for Intel

The ZIP artifacts contain the complete `DigiEmu.app` bundle.

### Public release

Push a version tag such as `v0.2.0`. The workflow builds both architectures, runs the bundled self-test, and attaches the two ZIP files to the GitHub Release.

## Why this must build on macOS

The application bundle contains macOS-native binaries, including the patched `libunicorn.2.dylib` and the Python/GUI runtime. Those binaries cannot be substituted with the Windows DLL from the original release.

The workflow deliberately builds on real GitHub-hosted macOS runners: `macos-15` for arm64 and `macos-15-intel` for x86_64. GitHub documents both runner labels as available standard macOS runners.
