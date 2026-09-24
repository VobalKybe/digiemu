# DigiEmu on macOS

DigiEmu is distributed here as a native standalone `DigiEmu.app`. The emulator
architecture is kept intact; the Windows `winmm` audio path is replaced on
macOS by PortAudio/CoreAudio through `sounddevice`.

## Install

1. Download the ZIP matching your Mac: **arm64** for Apple Silicon or
   **x86_64** for Intel.
2. Unzip it and move `DigiEmu.app` to Applications if desired.
3. Launch it. An unsigned build may require Control-click -> Open on the first
   launch.

## Build locally

Install Xcode Command Line Tools, Homebrew CMake, Git and Python 3.12+, then:

    ./tools/build-macos.sh

The output is `build-macos/out/DigiEmu.app`.

## Why standalone first instead of VST3?

The current DigiEmu UI and emulator own the machine loop, framebuffer, session
files, MIDI/UI interaction and audio device. A VST3 plug-in must instead hand
a host-controlled audio/MIDI callback and cannot simply wrap this process.
Therefore the supported Mac deliverable here is the native app. A genuine VST3
port should be a second layer that moves the emulator audio engine behind a
VST3 processor interface; a launcher-shaped VST3 would not provide the correct
DAW behaviour.
