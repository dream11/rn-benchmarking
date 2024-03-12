# RN Benchmarking

This repository can be used for benchmarking react-native versions for old and new architecture on sample app.

## Prerequisite

1. [React Native Environment Setup](https://reactnative.dev/docs/next/environment-setup)
2. [Maestro Setup](https://maestro.mobile.dev/)
3. [Flashlight Setup](https://docs.flashlight.dev/)

## Setup

```
git clone https://github.com/dream11/rn-benchmarking.git
cd Benchamrking
yarn install
```

---

## Benchmarking Old Architecture

### Android:

1. Before running benchmarking on old architecture we need to make sure it's enabled.
2. Open android/gradle.properties and make sure **newArchEnabled** is set to **false**.
3. Run app using `yarn android`.
4. The benchamrking numbers can be found under **ExternalDirectoryPath** of emulator storage.
5. The path will be **/storage/emulated/0/Android/data/com.benchamrking/files/oldarch.json**

### iOS:

1. Before running benchmarking on old architecture we need to make sure it's enabled.
2. Run the following command to enable old architecture.
   ```
   cd ios
   export NO_FLIPPER=1 && bundle install && bundle exec pod install
   rm -rf build
   ```
3. Run app using `yarn ios`.
4. The benchmarking numbers can be found under app's **DocumentDirectoryPath**.
5. To get access to app's document directory run the following command:
   ```
   open $(xcrun simctl get_app_container booted com.benchamrking data)
   ```
6. After running the above benchamrking numbers can be found under **Documents/oldarch.json**.

---

## Benchmarking New Architecture

### Android:

1. Before running benchmarking on old architecture we need to make sure it's enabled.
2. Open android/gradle.properties and make sure **newArchEnabled** is set to **true**.
3. Run app using `yarn android`.
4. The benchamrking numbers can be found under **ExternalDirectoryPath** of emulator storage.
5. The path will be **/storage/emulated/0/Android/data/com.benchamrking/files/newarch.json**

### iOS:

1. Before running benchmarking on old architecture we need to make sure it's enabled.
2. Run the following command to enable old architecture.
   ```
   cd ios
   export NO_FLIPPER=1 && bundle install && RCT_NEW_ARCH_ENABLED=1 bundle exec pod install
   rm -rf build
   ```
3. Run app using `yarn ios`.
4. The benchmarking numbers can be found under app's **DocumentDirectoryPath**.
5. To get access to app's document directory run the following command:
   ```
   open $(xcrun simctl get_app_container booted com.benchamrking data)
   ```
6. After running the above benchamrking numbers can be found under **Documents/newarch.json**.

---

## Automation

1. Getting benchmarking number's manually by clicking on buttons sometimes be tedious.
2. In order to resolve this we have provided some automations scripts that can do this job for you.
3. This scripts will help getting numbers for time taken to render N views, texts, images component and flashlight score for spin animations of N views.
5. Run the following to get rendering time of N views, texts, images (tested on Android emulator & iOS Simulator):
   ```
    yarn get:numbers:android <IterationCount>
    // Example: yarn get:numbers:android 10
    yarn get:numbers:ios <IterationCount>
    // Example: yarn get:numbers:ios 10
   ```
6. Run the following command to get flashlight score (supported only on Android):
   ```
   yarn get:flashlight:score
   ```

> NOTE: 1. Benchmarking numbers can be found at same locations for respective platform's as specfied above. 2. Flashlight report can be found under **Reports** directory with name **flashlightscore.json**.
