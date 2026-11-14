# Feni Blood Donate Association (FBDA) — Android APK Project

This directory is a complete, ready-to-build Android Studio project wrapping your FBDA HTML application with:

- **Embedded App Logo**: Generated directly from the logo inside your attached HTML across `mdpi`, `hdpi`, `xhdpi`, `xxhdpi`, `xxxhdpi`, and Adaptive `anydpi-v26` launcher icons.
- **Background Running Support**: `ForegroundKeepAliveService` (`dataSync|mediaPlayback` foreground service + audio playback) + `WorkManager` `BackgroundSyncWorker` + `BootReceiver` (restarts monitoring after device reboot).
- **Actionable Notifications & FCM Push**: Android 13+ `POST_NOTIFICATIONS` runtime permission, high-importance `fbda_urgent_alerts` channel, deep-linking & `Call Now` / `Dismiss` actions, and Firebase Cloud Messaging (`app/google-services.json` pre-attached for `fbda-6e92f`).
- **Over-The-Air (OTA) HTML Updates**: Checks your OTA manifest URL at startup, periodically in `BackgroundSyncWorker`, and on demand from Account Settings (`OtaHtmlUpdater.kt`).
- **Accessibility & Font Size Support**: `MainActivity` syncs Android `resources.configuration.fontScale` to `WebView.settings.textZoom` (85%–200%) and updates CSS `--fbda-font-scale` live in `assets/index.html`.

---

## Option B (Recommended): Cloud Build via GitHub Actions (No Android Studio Needed)

1. Unzip `FBDA-Android-APK-Project.zip` so you have the `FBDA-Android-APK/` folder (which already includes `.github/workflows/build-apk.yml` and `app/google-services.json`).
2. Create a new empty GitHub repository (private or public) and push the contents of `FBDA-Android-APK/` to `main`:
   ```bash
   cd FBDA-Android-APK
   git init -b main
   git add -A
   git commit -m "Initial FBDA Android APK project"
   git remote add origin https://github.com/<YOUR_USERNAME>/<YOUR_REPO>.git
   git push -u origin main
   ```
   *(Important: Use `git add -A` so the hidden `.github/workflows/build-apk.yml` folder is included.)*
3. In GitHub, open **Actions &rarr; Build FBDA Android APK** (it triggers automatically on push, or click **Run workflow** anytime to choose `debug` or `both`).
4. Once the green checkmark completes (~2–3 minutes), scroll to **Artifacts** at the bottom of the workflow run and download **`FBDA-Blood-Donate-Debug-APK`** containing `app-debug.apk`.

---

## Option A: Build Locally in Android Studio
1. Unzip the downloaded archive and open `FBDA-Android-APK/` in **Android Studio**.
2. Wait for Gradle Sync to complete (`app/google-services.json` is already detected automatically).
3. Click **Build &gt; Build Bundle(s) / APK(s) &gt; Build APK(s)**.
4. Your `.apk` is created at `app/build/outputs/apk/debug/app-debug.apk`.
