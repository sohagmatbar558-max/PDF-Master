# Google AdMob Integration Guide — PDF Master

## 1. Official Google Test Ad Unit IDs (Pre-Configured)
During development and emulator testing, `PDF Master` strictly uses Google's official test IDs in `AndroidManifest.xml` and `res/values/strings.xml` so your AdMob account is never flagged for invalid traffic:

- **App ID (Test)**: `ca-app-pub-3940256099942544~3347511713`
- **Banner Ad Unit**: `ca-app-pub-3940256099942544/6300978111`
- **Interstitial Ad Unit**: `ca-app-pub-3940256099942544/1033173712`
- **Rewarded Ad Unit**: `ca-app-pub-3940256099942544/5224354917`

## 2. Non-Disruptive Ad Policy Architecture
Implemented in `com.pdfmaster.tools.ads.AdMobManager`:
1. **Banner Ads**: Anchored exclusively to the bottom bar of `HomeScreen` — never inside the `PdfReaderScreen` reading canvas or overlapping buttons.
2. **Interstitial Frequency Cap**: Enforces a hard **90-second cooldown** (`INTERSTITIAL_COOLDOWN_MS = 90_000L`) and triggers **only after** a user-initiated export/conversion finishes, never on app launch or back navigation.
3. **Rewarded Video**: Optional user-initiated opt-in inside **Settings & Help** to unlock Ad-Free Pro mode.
4. **Pro Mode Bypass**: When `isPro == true`, `AdMobManager` and `BannerAdBar` skip ad requests completely.

## 3. Switching to Production Before Google Play Release
1. Create an app in your [Google AdMob Console](https://admob.google.com/).
2. Replace `com.google.android.gms.ads.APPLICATION_ID` in `AndroidManifest.xml` with your real App ID.
3. Replace the three unit IDs in `app/src/main/res/values/strings.xml` with your production Banner, Interstitial, and Rewarded Unit IDs.
4. Connect `SettingsAndHelpScreen` to Google Play Billing Library (`com.android.billingclient:billing-ktx`) for the one-time "Remove Ads" IAP product.
