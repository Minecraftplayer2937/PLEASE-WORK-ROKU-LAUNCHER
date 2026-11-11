# Roku Launcher

An Android TV home-screen replacement that recreates the look and feel of several eras of the Roku home screen (2008, 2013, Roku 4 flat, 2024, 2026), built with Jetpack Compose. Layout is done on a fixed 960 x 540 dp canvas so it looks the same on any TV resolution.

## Features
- Era-accurate menus: 2008 horizontal strip, 2013 / Roku 4 static sidebar, 2024 / 2026 pinned endless sidebar
- Launches Leanback apps (falls back to regular launcher apps)
- Settings (press Menu): menu style, tile size, wallpaper
- Registers as a HOME app, so it can be set as the default launcher

## Project structure
```
RokuLauncher/
├── .github/workflows/main.yml   # CI: builds debug APK
├── .gitignore
├── .gitattributes
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
└── app/
    ├── build.gradle.kts
    └── src/main/
        ├── AndroidManifest.xml
        ├── res/values/themes.xml
        └── java/com/example/rokulauncher/
            ├── MainActivity.kt     # entry point, key handling, state
            ├── Era.kt              # per-era layout profiles
            ├── Sidebar.kt          # sidebar rendering (pinned / static)
            ├── StripHome.kt        # 2008 strip layout
            ├── HomePane.kt         # app tile grid + "Jump To"
            ├── SettingsScreen.kt   # launcher settings overlay
            ├── AppsRepo.kt         # installed app discovery
            ├── Prefs.kt            # SharedPreferences
            └── Wallpaper.kt        # wallpaper styles
```

## Build
Open in Android Studio (Koala or newer) and let it sync, or from a terminal with Gradle 8.7:

```
gradle assembleDebug
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

CI: every push to `main` builds a debug APK via GitHub Actions (`.github/workflows/main.yml`). Download it from the run's Artifacts section.

Optional: run `gradle wrapper --gradle-version 8.7` once and commit `gradlew`, `gradlew.bat` and `gradle/wrapper/` so others can build without installing Gradle.

## Requirements
- JDK 17, Android SDK 34, minSdk 26
