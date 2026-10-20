# chiaki-ng for Android (unofficial build)

**PS4 / PS5 Remote Play on your Android phone or tablet.** This repository publishes a signed Android APK of [chiaki-ng](https://github.com/chiaki-ng/chiaki-ng). It is not the PC version: for Linux, Windows, macOS or Steam Deck, use the [official chiaki-ng project](https://github.com/chiaki-ng/chiaki-ng).

### Install

- **Komi Store (recommended):** search for `Raid-Made/chiaki-ng` in [Komi Store](https://github.com/kurikomi-labs/komi-store) and install. Komi offers each new release as an update.
- **Manual:** download the `.apk` from the [latest release](https://github.com/Raid-Made/chiaki-ng/releases/latest) and open it on your device.

Updates keep your registered consoles and settings. Every release uses the same package ID (`com.raidmade.chiaking`) and signing key, so Android installs it over the existing app. Don't uninstall first, or you'll lose your console registration.

The package ID is separate from the older `com.metallic.chiaki` app, so both can be installed side by side.

### What's different in this build

- On-screen touch controls work again (buttons, D-pad, sticks and touchpad).
- **Settings → On-Screen Controls** turns the touch overlay off when you use a physical controller.

Build and release details: [ANDROID_RELEASE.md](ANDROID_RELEASE.md).

Android build maintained by [Raid-Made](https://github.com/Raid-Made), built together with Claude (Anthropic). chiaki-ng itself is the work of the [chiaki-ng project](https://github.com/chiaki-ng/chiaki-ng).

---

*Everything below is the upstream chiaki-ng README.*


![chiaki-ng Logo](gui/res/chiaking-logo.svg)

# [chiaki-ng](https://streetpea.github.io/chiaki-ng/)

An open source PlayStation remote play project serving as the next-generation of Chiaki with improvements and ongoing support now that the original Chiaki project is in maintenance mode only. [Click here to see the accompanying site for documentation, updates and more](https://streetpea.github.io/chiaki-ng/).

## Discord
[chiaki-ng community Discord](https://discord.gg/tAMbRuwXDH)

## Disclaimer
This project is not endorsed or certified by Sony Interactive Entertainment LLC.

Chiaki is a Free and Open Source Software Client for PlayStation 4 and PlayStation 5 Remote Play
for Linux, FreeBSD, OpenBSD, Android, macOS, Windows, Nintendo Switch and potentially even more platforms.
