Android EmojiCompat Sample (Kotlin)
===================================

A quick demonstration of the various ways to
[Support Modern Emoji](https://developer.android.com/develop/ui/views/text-and-emoji/emoji2) using
Google's EmojiCompat library

Source initially copied from
[android/user-interface-samples/EmojiCompat](https://github.com/android/user-interface-samples/tree/main/EmojiCompat)

## Dependency Versions

| library   | version |
|-----------|---------|
| appcompat | 1.5.1   |
| emoji2    | 1.2.0   |

## Demo Apps

### app-emojicompat-appcompat

Using AppCompat [to support the latest emoji](https://developer.android.com/develop/ui/views/text-and-emoji/emoji2#appcompat).
AppCompat will invoke `EmojiCompatInitializer` at app startup.

### app-emojicompat-bundled

Bundling the _Noto Color Emoji Compat_ font by way of the `emoji2-bundled` artifact, as described
[here](https://developer.android.com/develop/ui/views/text-and-emoji/emoji2#support-bundled-fonts).
* Invoking `EmojiCompat.init(BundledEmojiCompatConfig(..))` during `Application.onCreate`.
* Manifest provider for `EmojiCompatInitializer` is still present. Removing this as described
[here](https://developer.android.com/develop/ui/views/text-and-emoji/emoji2#use-different-font-provider)
breaks the integration.

### app-emojicompat-fontrequest

Launching a Font Request to download the _Noto Color Emoji Compat_ font by initializing EmojiCompat
with `FontRequestEmojiCompatConfig`.
* Following the FontRequest flow as demonstrated in the
[Android EmojiCompat Sample project](https://github.com/android/user-interface-samples/tree/main/EmojiCompat)
* Removed the Manifest provider for `EmojiCompatInitializer` as described [here](https://developer.android.com/develop/ui/views/text-and-emoji/emoji2#use-different-font-provider)

## Tests

EmojiCompat configurations that rely on FontRequest do not appear functional on an Android 11
Emulator with up-to-date Google Play Services. The steps to resolve this issue provided
[here](https://developer.android.com/develop/ui/views/text-and-emoji/emoji2#use-different-font-provider)
have not resolved the issue.

Test: Multi-skin-toned handshake emoji should render successfully: ???????????????????

Result: Only renders when EmojiCompat is initialized with `BundledEmojiCompatConfig`

| Device                                       | AppCompat                                                                                 | Bundled | FontRequest |
|----------------------------------------------| ------------------------------------------------------------------------------------------|---------|-------------|
| ??? Emulator<br>Android 11<br>(Pixel 4 with Playstore)<br>Running recent<br>version (22.39.15)<br> of Playstore | <img alt="app-emojicompat-appcompat" src="img/app-emojicompat-appcompat.png" width=220 /> | <img alt="app-emojicompat-bundled" src="img/app-emojicompat-bundled.png" width=220 /> | <img alt="app-emojicompat-fontrequest" src="img/app-emojicompat-fontrequest.png" width=220 /> |
| ??? Real Device<br>Android 11<br>One Plus | <img alt="real-device-app-emojicompat-appcompat" src="img/real-device-app-emojicompat-appcompat.png" width=220 /> | <img alt="real-device-app-emojicompat-bundled" src="img/real-device-app-emojicompat-bundled.png" width=220 /> | <img alt="app-emojicompat-fontrequest" src="img/real-device-app-emojicompat-fontrequest.png" width=220 /> |


## To Build

```
./gradlew assembleDebug
adb install -r -t ./app-emojicompat-bundled/build/outputs/apk/debug/app-emojicompat-bundled-debug.apk
adb install -r -t ./app-emojicompat-fontrequest/build/outputs/apk/debug/app-emojicompat-fontrequest-debug.apk
adb install -r -t ./app-emojicompat-appcompat/build/outputs/apk/debug/app-emojicompat-appcompat-debug.apk
```
