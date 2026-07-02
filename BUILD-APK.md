# Build the Cargo Mate APK with GitHub 

GitHub builds the Android `.apk` for you in the cloud — no Android Studio needed.

## What gets uploaded to GitHub
Put these in the repository (the `www` folder is your app):

```
www/                       <- the app (index.html, icons, sw.js, manifest, ship.svg)
package.json
capacitor.config.json
.gitignore
.github/workflows/build-apk.yml
```

(`node_modules/` and `android/` are generated during the build — don't upload them; they're in `.gitignore`.)

## Steps

1. **Create a repo** at github.com (e.g. `cargomate`). It can be private.
2. **Upload the files above.** Easiest in the browser: open the repo → *Add file → Upload files* → drag the folder contents in → Commit. (Make sure the `www` folder and the `.github` folder are included.)
3. GitHub automatically starts the build. Open the **Actions** tab and watch *"Build Android APK"*. (You can also press *Run workflow* there to build on demand.)
4. When it finishes (a few minutes), open that workflow run, scroll to **Artifacts**, and download **CargoMate-apk**. Inside is `app-debug.apk`.

## Install on the phone
- Copy `app-debug.apk` to the Android phone.
- Tap it; allow **"Install unknown apps"** if prompted.
- Cargo Mate installs like a normal app, runs full-screen and offline.

## Notes
- This is a **debug-signed** APK — perfect for installing on your own / crew phones by sideloading. (A Play-Store release build would need a signing key; ask if you want that added.)
- To change the app name or ID, edit `capacitor.config.json` (`appName`, `appId`).
- After you update `www/index.html`, just commit the change — GitHub rebuilds a fresh APK.
