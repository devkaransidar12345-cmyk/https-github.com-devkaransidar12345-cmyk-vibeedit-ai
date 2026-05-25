# VibeEdit AI - Android APK Build Guide

## Prerequisites

Before building, ensure you have:
- Node.js 16+ and npm installed
- Expo CLI installed (`npm install -g expo-cli`)
- EAS CLI installed (`npm install -g eas-cli`)
- Expo account (create at https://expo.dev)
- Android SDK (if building locally)

## Step 1: Install Dependencies

```bash
npm install
```

This installs all required packages including:
- `expo` - Core Expo framework
- `react-native` - React Native framework
- `expo-camera` - Camera module for photo editing
- Navigation libraries
- Development tools

## Step 2: Configure EAS Account

```bash
eas login
# or
eas register
```

Login with your Expo account credentials.

## Step 3: Link Project to EAS

```bash
eas project:init
# This creates an Expo project on the cloud and links it to your local project
```

## Step 4: Generate Android APK

### Option A: Cloud Build (Recommended - No Android SDK Required)

```bash
eas build --platform android
```

This will:
1. Create a cloud build on Expo's servers
2. Compile your Expo app for Android
3. Generate a signed APK
4. Provide a download link when complete

Monitor progress:
```bash
eas build:list  # View all builds
eas build:view <build-id>  # View specific build details
```

### Option B: Local Build (Requires Android SDK)

```bash
npm run prebuild
# This generates the native Android project

npm run build:android
```

## Step 5: Test the APK

Once the build completes:

1. **Download the APK** from the provided link
2. **Install on device**:
   ```bash
   adb install path/to/vibeedit-ai.apk
   ```
3. **Launch the app** from your device

## Troubleshooting

### Issue: Build fails with dependency errors
**Solution:**
```bash
npm install --no-save
rm -rf node_modules
npm install
eas build --platform android --clear-cache
```

### Issue: Android SDK not found
**Solution:**
- Install Android Studio from https://developer.android.com/studio
- Set ANDROID_HOME environment variable:
  ```bash
  export ANDROID_HOME=$HOME/Library/Android/sdk
  export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
  ```

### Issue: Gradle build fails
**Solution:**
```bash
expo prebuild --clean
eas build --platform android --clear-cache
```

### Issue: Signing certificate error
**Solution:**
```bash
eas credentials -p android
# Follow prompts to create/update credentials
```

## Build Variants

### Development APK
```bash
eas build --profile development --platform android
```

### Preview APK
```bash
eas build --profile preview --platform android
```

### Production APK (for Play Store)
```bash
eas build --profile production --platform android
```

## Next Steps

1. **Test APK thoroughly** on real Android devices
2. **Update app version** in `app.json` for new builds
3. **Add code signing credentials** for production builds
4. **Submit to Google Play Store** when ready:
   ```bash
   eas submit -p android --latest
   ```

## Useful Commands

```bash
# Start development server
npm start

# Run on Android emulator
npm run android

# View build logs
eas build:view <build-id> --log

# List available devices
adb devices

# Install APK manually
adb install -r app.apk

# Clear Expo cache
expo start --clear
```

## Documentation

- [Expo Documentation](https://docs.expo.dev)
- [EAS Build Documentation](https://docs.expo.dev/build/introduction/)
- [React Native Docs](https://reactnative.dev)
- [Android Development](https://developer.android.com)

## Support

For issues:
1. Check [Expo Discord](https://discord.gg/expo)
2. Visit [GitHub Issues](https://github.com/expo/expo/issues)
3. Check [Stack Overflow](https://stackoverflow.com/questions/tagged/expo)
