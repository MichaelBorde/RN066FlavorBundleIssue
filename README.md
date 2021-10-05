# RN066FlavorBundleIssue

React Native (`0.66`) project to demonstate an issue with JS bundle and android flavors.

The issue is about a missing JS bundle in some flavored apks.

It is based on standard template (`npx react-native init`) with minimal modifications in `android/app/build.gradle` to define flavors.

## How to reproduce issue

```
cd android
./gradlew clean assembleRelease
```

Run this command to see the generated apks (1 per flavor):

```
find . -name "*.apk"                                   
```

Which outputs:

```
./app/build/outputs/apk/dog/release/app-dog-release.apk
./app/build/outputs/apk/cat/release/app-cat-release.apk
```

Unzip to check if js bundle is present:

```
find . -name "*.apk" -exec unzip -l {} \; | grep assets
```

Which outputs:

```
760777  1981-01-01 01:01   assets/index.android.bundle
```

(Only 1 occurence)

Though expected ouput should be:

```
760777  1981-01-01 01:01   assets/index.android.bundle
760777  1981-01-01 01:01   assets/index.android.bundle
```

(2 occurences)