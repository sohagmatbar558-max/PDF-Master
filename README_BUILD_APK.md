# Building & Installing the PDF Master APK (`com.pdfmaster.tools`)

## Prerequisites
- **Android Studio** Ladybug (2024.2+) or newer
- **JDK 17** (bundled with Android Studio)
- **Android SDK Platform 35** & Build-Tools 35.0.0

## Method 1: Android Studio (GUI)
1. Open Android Studio and select **Open**.
2. Choose the `android/` directory from the downloaded project archive.
3. Wait for Gradle sync to finish (`libs.versions.toml` resolves Compose, ML Kit Document Scanner, DataStore, and Google Play Services Ads).
4. To build a test APK: **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
   - Output location: `app/build/outputs/apk/debug/app-debug.apk`
5. To build a Play Store Release APK/AAB: **Build → Generate Signed App Bundle / APK**.

## Method 2: Command Line (Gradle + ADB)
```bash
cd android
./gradlew assembleDebug
adb install -r app/build/outputs/apk/debug/app-debug.apk
```

For a release APK:
```bash
./gradlew assembleRelease
```
