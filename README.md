# Canopy: build the Windows .exe and Android .apk

The app itself is the single file `www/index.html`. This project wraps it for both platforms.

## Easiest way: let GitHub build both files for free

1. Create a free account at github.com and make a new empty repository (private is fine).
2. Upload everything in this folder to it, including the hidden `.github` folder.
   (On the repository page: Add file > Upload files. Drag the whole folder contents in.)
3. Open the repository's **Actions** tab, choose **Build Canopy**, and press **Run workflow**.
4. Wait about 5 to 10 minutes. Open the finished run and download:
   - **Canopy-Windows**: the .exe files (a portable `Canopy.exe` and an installer)
   - **Canopy-Android**: `app-debug.apk`

### Installing
- **Laptop:** run the portable .exe, or the installer. Windows may show a "protected your PC" warning because the file is not code-signed. Choose More info, then Run anyway.
- **Phone:** copy `app-debug.apk` to the phone and open it. Android will ask to allow installs from this source. Allow it for your file manager or browser.

## Build on your own computer instead

Needs Node.js 20 or newer.

    npm install
    npm start              # try the desktop app
    npm run build:win      # makes dist/*.exe (run this on Windows)

For the APK you also need Android Studio (or JDK 17 plus the Android SDK):

    npm install
    npx cap add android
    npx cap sync android
    cd android && ./gradlew assembleDebug

The APK ends up in `android/app/build/outputs/apk/debug/app-debug.apk`.

## Notes
- Your sessions, coins and trees are stored on the device. The laptop and phone versions do not sync with each other. Use Settings > Your data to copy a backup from one and restore it on the other.
- The text fonts load from Google Fonts when online and fall back to system fonts offline.
- The APK is a debug build for sideloading. Putting it on the Play Store needs a signed release build and a developer account.
