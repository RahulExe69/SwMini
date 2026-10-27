# Swordigo Unbound — Modding Roadmap

## Project goal

Build an original Swordigo mod using SwMini's existing engine hooks, Lua extensions, configuration,
and resource-replacement system. Treat RLSwordigo as inspiration, not as a source-code dependency:
its complete implementation is not available in the public repository we inspected.

## Current foundation

- Working title: **Swordigo Unbound**.
- Base game targeted by the underlying SwMini framework: **Swordigo 1.4.12, build 47**.
- Unique Android application ID: `net.rahulexe.swordigounbound`, so the mod can be installed separately from the original app.
- First configuration experiment: increase the Soul Shard limit to **65,535**, which is the maximum documented by SwMini's `Mini.SetCoinLimit` API.
- Build and gameplay status: **not yet verified**. A successful GitHub commit is not the same as a successful APK build or an in-game test.

## Build prerequisite

SwMini intentionally does not distribute the copyrighted game resources, compiled game libraries, or original compiled classes. The build scripts extract those from a compatible local APK, so this repository cannot produce a complete APK until the developer supplies the matching game APK.

1. Install Git and a compatible JDK/Android SDK/NDK setup, or open the project in Android Studio.
2. Clone the repository and initialize its submodules:
   ```sh
   git clone https://github.com/RahulExe69/SwMini.git
   cd SwMini
   git submodule update --init --recursive
   ```
3. Use a legitimate Swordigo APK that matches the framework's documented target, and keep it outside version control. Extract the required files:
   ```sh
   ./gradlew :app:extractVanilla -Path="/absolute/path/to/swordigo.apk"
   ```
4. Assemble the app:
   ```sh
   ./gradlew :app:assembleDebug
   ```
   If extraction fails, check the APK version and confirm it contains both `arm64-v8a` and `armeabi-v7a` native libraries.
5. Install the debug APK on a test device, launch it, and inspect Android Logcat for native or Lua errors. Back up saves before testing.

Do **not** commit `vanilla.apk`, extracted game resources, proprietary native libraries, or a built APK. The project ignores APK files and extracted build products for a reason.

## Roadmap

### Milestone 1 — Baseline (in progress)
- [x] Create our own mod identity and application ID.
- [x] Add the first low-risk configuration experiment: expanded Soul Shard cap.
- [ ] Build from a matching local APK.
- [ ] Confirm the app launches and the configured cap takes effect in-game.

### Milestone 2 — First scripted feature
- [ ] Inspect existing scene/script resources and identify a well-understood Lua extension point.
- [ ] Add one small, reversible Lua feature with logging and a simple way to disable it.
- [ ] Test normal gameplay, scene transitions, and save/load behaviour.

### Milestone 3 — Original content
- [ ] Investigate supported scene, model, texture, and audio resource formats.
- [ ] Add original or properly licensed assets and a custom gameplay object.
- [ ] Explore custom enemy/boss behaviour only after scene scripts and entity APIs are understood.

### Milestone 4 — Release engineering
- [ ] Record the exact base-game version and tested device architectures for each release.
- [ ] Add automated checks that do not require proprietary game files.
- [ ] Design an APK build process that obtains the required game files locally without publishing them.
- [ ] Publish versioned releases only after the APK is built and tested.

## Licensing and attribution

SwMini is GPL-3.0 licensed; preserve its license and required attribution when modifying or redistributing its covered code. Swordigo remains a separate proprietary game. Never publish the original game APK or extracted copyrighted assets as part of this project.