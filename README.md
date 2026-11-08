# PocketWise – Student Money Manager

One codebase, four ways to run it:

| Platform | How | Output |
|---|---|---|
| Web / any phone or PC | GitHub Pages workflow | Installable PWA (iPhone: Share → Add to Home Screen) |
| Android | Capacitor + `android.yml` | `app-debug.apk` |
| Windows | Electron + `windows.yml` | `.exe` installer and portable `.exe` |
| iOS | Capacitor + `ios.yml` | Unsigned simulator build (see signing note) |

## Put it on GitHub
```bash
cd pocketwise-app
git init -b main
git add .
git commit -m "PocketWise first commit"
git remote add origin https://github.com/<your-username>/pocketwise.git
git push -u origin main
```
(Create the empty repo `pocketwise` on github.com first.)

## Get your apps
1. **Web:** repo → Settings → Pages → Source: *GitHub Actions*. The site goes live at `https://<your-username>.github.io/pocketwise/` after the workflow runs.
2. **Android / Windows:** repo → Actions → run *Build Android APK* / *Build Windows app* (they also run on every push). Download the file from the run's **Artifacts**.
3. **iOS:** repo → Actions → *Build iOS*. A real iPhone install or App Store release needs an Apple Developer account ($99/yr) and signing in Xcode. Until then, use the web app on iPhone.

## Run locally
```bash
npm install
npm start            # opens the Windows/desktop app in Electron
npx cap add android && npx cap sync android && npx cap open android
```

## Good to know
- Data is stored **on the device** (localStorage). The cloud sync in the claude.ai version needs claude.ai, so it is not available here. To add real cloud sync, connect Firebase or Supabase in `www/index.html` (`initStore()` is the only function to replace).
- Email + password login is a local lock on the device. Every device keeps its own account.
- The Android APK is a debug build. For Play Store you need a signed release build.
