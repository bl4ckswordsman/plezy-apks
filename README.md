# Plezy APK Releases

[![Extract Plezy APKs](https://github.com/bl4ckswordsman/plezy-apks/actions/workflows/extract.yaml/badge.svg)](https://github.com/bl4ckswordsman/plezy-apks/actions/workflows/extract.yaml)
[![Update F-Droid Repo](https://github.com/bl4ckswordsman/plezy-apks/actions/workflows/fdroid.yml/badge.svg)](https://github.com/bl4ckswordsman/plezy-apks/actions/workflows/fdroid.yml)

Standalone `.apk` files automatically extracted from [edde746/plezy](https://github.com/edde746/plezy) releases — ready to install via F-Droid, Obtainium, or direct download.

## Install via F-Droid

Visit the **[F-Droid repo landing page](https://bl4ckswordsman.github.io/plezy-apks/)** — tap the link to add the repo directly in your F-Droid client, or scan the QR code.

<details>
<summary><strong>Manual setup</strong></summary>

Add this URL in F-Droid or a compatible client (e.g. [Droid-ify](https://github.com/Droid-ify/client)):

```
https://bl4ckswordsman.github.io/plezy-apks/fdroid/repo
```

1. Open F-Droid (or Droid-ify)
2. Go to **Settings → Repositories → Add repository**
3. Paste the URL above
4. Search for **Plezy** and install

</details>

## Install via Obtainium

[![Get it on Obtainium](https://raw.githubusercontent.com/ImranR98/Obtainium/main/assets/graphics/badge_obtainium.png)](http://apps.obtainium.imranr.dev/redirect.html?r=obtainium://add/https://github.com/bl4ckswordsman/plezy-apks/releases)

<details>
<summary><strong>Expand Instructions</strong></summary>

1. Open Obtainium
2. Tap **Add App**
3. Paste this URL:
   ```
   https://github.com/bl4ckswordsman/plezy-apks
   ```
4. Set **APK filter regex** to match your device:
   - `arm64-v8a` — most modern phones *(recommended)*
   - `armeabi-v7a` — older 32-bit devices
   - `x86_64` — emulators / ChromeOS
5. Done — Obtainium will auto-update Plezy for you

</details>

## Direct Download

Head to the [Releases](https://github.com/bl4ckswordsman/plezy-apks/releases/latest) page and grab the APK for your architecture.

| File | Architecture | Devices |
|------|-------------|---------|
| `plezy-android-arm64-v8a.apk` | ARM 64-bit | Most modern phones & tablets |
| `plezy-android-armeabi-v7a.apk` | ARM 32-bit | Older Android devices |
| `plezy-android-x86_64.apk` | x86_64 | Emulators, ChromeOS |

> **Not sure which one?** Almost all modern Android phones use `arm64-v8a`.

<details>
<summary><strong>Under the Hood (Why & How)</strong></summary>

### Why?
Since Plezy v1.13.0, Android builds are packaged as `.tar.gz` archives. This breaks Obtainium auto-updates and makes manual installation inconvenient. This repo automatically extracts the APKs daily and publishes them as proper GitHub releases, and also maintains an F-Droid-compatible repo served via GitHub Pages.

### How it works

**APK extraction** — runs daily and on-demand:
1. Checks the latest [Plezy release](https://github.com/edde746/plezy/releases)
2. Skips if the version is already published here
3. Downloads all Android `.tar.gz` archives
4. Extracts the `.apk` files
5. Creates a new GitHub release with standalone APKs + upstream changelog

**F-Droid repo** — triggers on each new release:
1. Downloads the APKs from the new GitHub release
2. Runs `fdroid update` to regenerate the signed index
3. Deploys the index + APKs to GitHub Pages (no binaries committed to git)

---

### Run It Yourself
Fork this repo or copy `.github/workflows/` into a new repo. The extract workflow needs no configuration — it works out of the box with the default `GITHUB_TOKEN`. The F-Droid workflow additionally requires these repository secrets: `KEYSTORE_BASE64`, `REPO_KEYALIAS`, `KEYPASS`, `KEYDNAME`.

</details>
