# Put Cargo Mate on an iPhone (Add to Home Screen)

The app is a PWA, so an iPhone installs it straight from Safari — no Mac, no
Xcode, no Apple Developer account, no App Store. You host the app once on a free
HTTPS web address (GitHub Pages), then each phone adds it to the Home Screen.

## One-time setup (on a computer, ~3 minutes)

1. Make sure the project is in a GitHub repo (the same one you use for the APK is
   fine). The file `.github/workflows/deploy-pages.yml` must be included.
2. In the repo, open **Settings -> Pages**.
3. Under **Build and deployment -> Source**, choose **GitHub Actions**. (You do
   NOT need to pick a branch.)
4. Open the **Actions** tab and let *"Deploy to GitHub Pages (iPhone PWA)"* run
   (it starts on every push; you can also press **Run workflow**).
5. When it finishes, the run shows your web address. It looks like:

   ```
   https://<your-github-username>.github.io/<repo-name>/
   ```

   (You can also find it any time under **Settings -> Pages**.)

That URL is your app. Bookmark it / send it to the crew.

## Install on each iPhone (~20 seconds)

1. Open the URL above in **Safari** (it must be Safari — Chrome on iOS can't
   install Home Screen apps).
2. Tap the **Share** button (the square with an up-arrow at the bottom).
3. Scroll down and tap **Add to Home Screen**.
4. Tap **Add** (top right).

Cargo Mate now sits on the Home Screen with its own icon, opens full-screen
(no Safari bars), and works offline after the first load.

## Updating the app later

Edit `www/index.html`, commit/push to GitHub. Pages rebuilds automatically.
On the phone, just open the app while online once and it picks up the new
version (the service worker refreshes the cache). If a phone seems stuck on an
old version, remove the Home Screen icon and Add to Home Screen again.

## Good to know on iOS

- **Camera** (CC photos): the first time you use it, iOS asks for camera
  permission — tap Allow. Works in the installed Home Screen app over HTTPS.
- **Offline & data**: bays, photos and notes are stored on the phone and work
  with no signal. iOS can clear a web app's storage if the app is not opened for
  a long time (a few weeks). To keep crew phones in sync and safe, set the same
  **Vessel sync code** on each phone (Settings -> gear) so data lives in the
  cloud too.
- **Must be HTTPS**: the GitHub Pages address is HTTPS, which is required for the
  camera and offline features. A plain file or http:// address will not work.

## Want a "real" App Store / TestFlight app instead?

That needs a Mac with Xcode and an Apple Developer account ($99/yr). The same
`www` app wraps into iOS with Capacitor (`npx cap add ios`). Ask and I'll add the
iOS build steps — but for crew use, Add to Home Screen above is faster and free.
