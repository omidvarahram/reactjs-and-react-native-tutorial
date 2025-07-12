# React Native Foundation Index

## 1. Introduction to React Native
- [1.1 What is React Native?](./context/001-introduction-to-react-native.md#11-what-is-react-native)
- [1.2 React Native vs React: Core Differences](./context/001-introduction-to-react-native.md#12-react-native-vs-react-core-differences)
- [1.3 The React Native Ecosystem](./context/001-introduction-to-react-native.md#13-the-react-native-ecosystem)
- [1.4 Architecture: JS Thread, Native Bridge, and Rendering](./context/001-introduction-to-react-native.md#14-architecture-js-thread-native-bridge-and-rendering)

## 2. Setting Up the Environment
- [2.1 Installing Node, npm, and Watchman](./context/002-setup-environment.md#21-installing-node-npm-and-watchman)
- [2.2 Choosing a Setup: Expo vs React Native CLI](./context/002-setup-environment.md#22-choosing-a-setup-expo-vs-react-native-cli)
- [2.3 Installing with React Native CLI (Android/iOS)](./context/002-setup-environment.md#23-installing-with-react-native-cli)
- [2.4 Installing with Expo CLI](./context/002-setup-environment.md#24-installing-with-expo-cli)
- [2.5 Setting Up Android Studio and Xcode Simulators](./context/002-setup-environment.md#25-setting-up-android-studio-and-xcode-simulators)
- [2.6 Connecting and Running on Physical Devices](./context/002-setup-environment.md#26-connecting-and-running-on-physical-devices)
- [2.7 Debugging Environment Issues](./context/002-setup-environment.md#27-debugging-environment-issues)

## 3. Project Structure & Native Files
- [3.1 Project Directory Overview](./context/003-project-structure.md#31-project-directory-overview)
- [3.2 The `android/` and `ios/` Folders](./context/003-project-structure.md#32-the-android-and-ios-folders)
- [3.3 Managing Assets (Fonts, Images, JSON)](./context/003-project-structure.md#33-managing-assets-fonts-images-json)

## 4. Styling in React Native
- [4.1 Inline Styles and StyleSheet.create](./context/004-styling-native.md#41-inline-styles-and-stylesheetcreate)
- [4.2 Flexbox in React Native](./context/004-styling-native.md#42-flexbox-in-react-native)
- [4.3 Platform-Specific Styling](./context/004-styling-native.md#43-platform-specific-styling)
- [4.4 Using Style Libraries (e.g., Tailwind, NativeBase)](./context/004-styling-native.md#44-using-style-libraries)

## 5. Core React Native Components
- [5.1 View, Text, ScrollView, FlatList](./context/005-core-components.md#51-view-text-scrollview-flatlist)
- [5.2 Touchable Components (TouchableOpacity, Pressable)](./context/005-core-components.md#52-touchable-components)
- [5.3 Image and SVG Handling](./context/005-core-components.md#53-image-and-svg-handling)
- [5.4 KeyboardAvoidingView and SafeAreaView](./context/005-core-components.md#54-keyboardavoidingview-and-safeareaview)

## 6. Platform APIs and Native Modules
- [6.1 Using `Platform`, `Dimensions`, and `PixelRatio`](./context/006-platform-apis.md#61-using-platform-dimensions-and-pixelratio)
- [6.2 Permissions and Native Capabilities](./context/006-platform-apis.md#62-permissions-and-native-capabilities)
- [6.3 Linking and Deep Linking](./context/006-platform-apis.md#63-linking-and-deep-linking)
- [6.4 Accessing Device Features (Camera, Location, etc)](./context/006-platform-apis.md#64-accessing-device-features)

## 7. Navigation in React Native
- [7.1 React Navigation Overview](./context/007-navigation.md#71-react-navigation-overview)
- [7.2 Stack, Tab, and Drawer Navigators](./context/007-navigation.md#72-stack-tab-and-drawer-navigators)
- [7.3 Navigation Props and Hooks](./context/007-navigation.md#73-navigation-props-and-hooks)
- [7.4 Linking and Navigation between Screens](./context/007-navigation.md#74-linking-and-navigation-between-screens)

## 8. State Management (Recap + RN Specifics)
- [8.1 React State and Context in RN](./context/008-state-management.md#81-react-state-and-context-in-rn)
- [8.2 AsyncStorage and Local Persistence](./context/008-state-management.md#82-asyncstorage-and-local-persistence)
- [8.3 Using Zustand or Redux with RN](./context/008-state-management.md#83-using-zustand-or-redux-with-rn)

## 9. Running the App
- [9.1 Running on iOS Simulator](./context/009-running-app.md#91-running-on-ios-simulator)
- [9.2 Running on Android Emulator](./context/009-running-app.md#92-running-on-android-emulator)
- [9.3 Live Reload, Fast Refresh, Hot Reload](./context/009-running-app.md#93-live-reload-fast-refresh-hot-reload)
- [9.4 Running on Physical Devices (USB/Wi-Fi)](./context/009-running-app.md#94-running-on-physical-devices)
- [9.5 Common Device Runtime Errors](./context/009-running-app.md#95-common-device-runtime-errors)

## 10. Networking and Data
- [10.1 Fetch, Axios, and Networking Setup](./context/010-networking.md#101-fetch-axios-and-networking-setup)
- [10.2 Handling Timeouts and Errors](./context/010-networking.md#102-handling-timeouts-and-errors)
- [10.3 Calling Native APIs (Bridging Concepts Intro)](./context/010-networking.md#103-calling-native-apis-bridging-concepts-intro)

## 11. Testing React Native
- [11.1 Unit Testing with Jest](./context/011-testing.md#111-unit-testing-with-jest)
- [11.2 UI Testing with React Native Testing Library](./context/011-testing.md#112-ui-testing-with-react-native-testing-library)
- [11.3 E2E Testing with Detox](./context/011-testing.md#113-e2e-testing-with-detox)
- [11.4 Mocking Native Modules](./context/011-testing.md#114-mocking-native-modules)

## 12. Debugging React Native
- [12.1 Debugging with Flipper](./context/012-debugging.md#121-debugging-with-flipper)
- [12.2 Chrome DevTools, Console, and Logs](./context/012-debugging.md#122-chrome-devtools-console-and-logs)
- [12.3 Handling Red Screens and Runtime Errors](./context/012-debugging.md#123-handling-red-screens-and-runtime-errors)
- [12.4 Performance Bottlenecks and Profiling](./context/012-debugging.md#124-performance-bottlenecks-and-profiling)

## 13. Deployment & Builds
- [13.1 Building for Production](./context/013-deployment.md#131-building-for-production)
- [13.2 Android: APK & AAB Generation](./context/013-deployment.md#132-android-apk--aab-generation)
- [13.3 iOS: App Store and TestFlight](./context/013-deployment.md#133-ios-app-store-and-testflight)
- [13.4 OTA Updates with Expo & CodePush](./context/013-deployment.md#134-ota-updates-with-expo--codepush)
- [13.5 App Signing and Security Keys](./context/013-deployment.md#135-app-signing-and-security-keys)

---

[⬅️ Back to Main Index](../../index.md)
