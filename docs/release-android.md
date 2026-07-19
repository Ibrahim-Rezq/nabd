# Android release (bundled APK — ADR-0013)

The APK bundles a static export of the app (`out/`). There is no OTA: every native release
is a rebuilt APK. Web deploys on Vercel do not reach installed apps.

## Build

```bash
pnpm cap:sync                      # build:native (static export, SW off) + capacitor sync android
cd android && ./gradlew assembleDebug    # or assembleRelease (needs signing config)
```

The debug APK lands in `android/app/build/outputs/apk/debug/app-debug.apk`. Signing and
release upload happen on the owner's machine, outside this repo (ADR-0012 §4).

**JDK 17 or 21 required.** The Gradle wrapper is 8.2.1 (bundled with Capacitor 6) and rejects
newer JDKs with `Unsupported class file major version …`. If your default `java` is newer
(e.g. 26), point the build at a supported JDK for that command only:

```bash
JAVA_HOME=/usr/lib/jvm/java-17-openjdk ./gradlew assembleDebug
```

## Per-release checklist

1. Bump `versionCode` (+1) and `versionName` (match `package.json` version) in
   `android/app/build.gradle`.
2. `pnpm cap:sync` exits 0 — a failing static export means something server-only crept into
   a page or a new route handler was added (see ADR-0013 consequences).
3. Verify `out/` contains the app routes and **no** `sw.js`.
4. Install on device, then in airplane mode force-stop and cold-start: the app must boot and
   render data from Dexie with zero network.
5. Prayer alarms re-arm on launch (ADR-0012 §2) and the adhan fires from a scheduled moment.
6. Sign-in roundtrip: system browser opens, `nabd://auth/callback` deep link returns to the
   app signed in (needs the redirect URL registered in the Supabase dashboard).
