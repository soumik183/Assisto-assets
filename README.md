# Assisto runtime assets

Runtime-downloaded binaries for the Assisto Android assistant. This repository is
public and contains **no application source code** — only prebuilt third-party
artifacts plus their checksums.

The Assisto app source lives in a private repository. These assets are published
here so that a device can fetch them over plain anonymous HTTPS, with no GitHub
authentication, no API token, and no rate limit.

## What is here

| File | Size | Purpose |
|---|---|---|
| `kittentts-native-arm64-v8a.so` | 1.7 MB | espeak-ng JNI bridge, ARM64 (most modern phones) |
| `kittentts-native-armeabi-v7a.so` | 1.3 MB | espeak-ng JNI bridge, ARMv7 (older 32-bit phones) |
| `kittentts-native-x86_64.so` | 1.6 MB | espeak-ng JNI bridge, x86_64 (emulators) |
| `espeak-ng-data.zip` | 604 KB | espeak-ng voice/timbre data |

Checksums for every file are in `SHA256SUMS`.

## Download URL

Assets are served from the `espeak-v1` release tag:

```
https://github.com/soumik183/Assisto-assets/releases/download/espeak-v1/<file>
```

## Why these are downloaded at runtime

The KittenTTS neural model (~24 MB) ships inside the APK. espeak-ng is only
needed to turn text into phonemes, so keeping it out of the APK keeps the
download small and lets a user delete it to reclaim space.

If this fetch fails, Assisto degrades gracefully to the Android system
TextToSpeech engine rather than failing silently.

## License — espeak-ng is GPLv3

The `.so` libraries here are built from [espeak-ng](https://github.com/espeak-ng/espeak-ng),
which is licensed under the **GNU General Public License v3**. See `NOTICE.md`.

The JNI glue and build wrapper that produce these libraries are part of the
Assisto application. The `espeak-ng-data.zip` payload is upstream espeak-ng data,
also GPLv3.