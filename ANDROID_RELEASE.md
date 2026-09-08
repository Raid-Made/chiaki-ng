# Chiaki-ng Android releases

This fork publishes an unofficial Android build of chiaki-ng as a consistently signed GitHub Release APK. The release format is intended to work well with Komi and other GitHub-release-based Android updaters.

## Android package

- Application ID: `com.raidmade.chiaking`
- FileProvider authority: `com.raidmade.chiaking.fileprovider`
- Release asset: `chiaki-ng-android-universal-<version>.apk`
- Workflow: `.github/workflows/android-release.yml`

The fork-specific package ID lets this build coexist with the older `com.metallic.chiaki` Android package.

## One-time signing setup

Keep the signing keystore permanently. Android only accepts an update when it is signed by the same certificate as the installed version. Losing the key means existing users cannot update to a replacement key without uninstalling the app first.

On Linux, create a private release key outside the repository:

```bash
mkdir -p ~/.local/share/chiaki-ng-android
chmod 700 ~/.local/share/chiaki-ng-android

keytool -genkeypair \
  -keystore ~/.local/share/chiaki-ng-android/release.jks \
  -storetype JKS \
  -alias chiaki-ng-android \
  -keyalg RSA \
  -keysize 4096 \
  -validity 10000
```

Back up `release.jks` somewhere secure. Do not commit it to Git.

## GitHub Actions secrets

The Android Release workflow requires these repository secrets:

- `ANDROID_KEYSTORE_BASE64`
- `ANDROID_KEYSTORE_PASSWORD`
- `ANDROID_KEY_ALIAS`
- `ANDROID_KEY_PASSWORD`

With GitHub CLI authenticated, upload the keystore without exposing it in shell history:

```bash
base64 -w0 ~/.local/share/chiaki-ng-android/release.jks \
  | gh secret set ANDROID_KEYSTORE_BASE64 -R Raid-Made/chiaki-ng

printf '%s' 'chiaki-ng-android' \
  | gh secret set ANDROID_KEY_ALIAS -R Raid-Made/chiaki-ng

read -rsp 'Keystore password: ' KS_PASS; echo
printf '%s' "$KS_PASS" \
  | gh secret set ANDROID_KEYSTORE_PASSWORD -R Raid-Made/chiaki-ng
printf '%s' "$KS_PASS" \
  | gh secret set ANDROID_KEY_PASSWORD -R Raid-Made/chiaki-ng
unset KS_PASS
```

The example assumes the key password is the same as the keystore password. If a different key password was chosen, upload that value separately as `ANDROID_KEY_PASSWORD`.

## Publishing a release

Run the workflow manually:

```bash
gh workflow run android-release.yml -R Raid-Made/chiaki-ng
```

The workflow:

1. checks out all submodules;
2. installs JDK 17, Android SDK 35, NDK r28c and CMake 3.22.1;
3. installs the nanopb Python dependencies;
4. builds a signed universal release APK;
5. verifies the APK signature with `apksigner`;
6. generates a SHA-256 checksum; and
7. creates the latest GitHub Release containing the APK and checksum.

The Android `versionCode` uses the UTC Unix timestamp so every later release has a greater version code. The visible version name includes the upstream chiaki-ng version and an Android build timestamp.

## Komi

After the first GitHub Release exists, users can link/search `Raid-Made/chiaki-ng` in Komi and select the `.apk` release asset. Future releases use the same package ID and signing certificate so Android and Komi can validate them as updates.
