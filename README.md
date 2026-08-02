# RIME

A tap/swipe puzzle game, packaged as an Android app with [Capacitor](https://capacitorjs.com/).

## Project layout

```
www/                     the game itself (index.html)
capacitor.config.json    Capacitor config (webDir = www, appId = studios.sorthan.rime)
package.json             npm deps: @capacitor/core, @capacitor/android, @capacitor/cli
.github/workflows/build.yml   GitHub Actions: builds a debug APK on every push to main
```

The `android/` native project is **not** committed — the workflow (and the
commands below) generate it fresh from `capacitor.config.json` every time.

## Build the APK automatically (GitHub Actions)

Just push this repo to GitHub. The workflow in `.github/workflows/build.yml`
will:

1. install npm deps
2. run `npx cap add android` (creates the android/ folder)
3. run `npx cap sync android` (copies `www/` into the native project)
4. run `./gradlew assembleDebug`
5. upload the resulting APK as a build artifact (**Actions → your run → Artifacts**)

You can also trigger it manually from the **Actions** tab (`workflow_dispatch`).

## Build locally

```bash
npm install
npx cap add android      # first time only
npx cap sync android      # after any change to www/
npx cap open android      # opens Android Studio, or:
cd android && ./gradlew assembleDebug
```

## Editing the game

Just edit `www/index.html`, then re-run `npx cap sync android` (or push to
GitHub — the workflow does this for you).
