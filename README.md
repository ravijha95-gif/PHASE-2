# PROJECT R — Phase 2 UI + Runtime Integration Preparation

PROJECT R is a personal Android launcher for a Windows-PC-game compatibility environment.

## What's new in Phase 2

- Premium dark gaming interface with cinematic gradient hero panel.
- New Home, Library, Engine and Settings navigation.
- Game tiles and detailed game overview.
- Import game folders through Android Storage Access Framework.
- Persistent library uses the same `project_r` preferences namespace as Phase 1.
- Remove imported folders from the library.
- Engine Center clearly reports which runtime components are not yet integrated.
- Device identity/ABI information shown in the Engine Center.
- GitHub Actions workflow detects either a repository-root Gradle project or a `project_r/` nested project.

## Important: runtime status

This Phase 2 package is the redesigned launcher and the integration-preparation milestone. It does **not** yet contain a runnable Wine/Box86/Box64/Mesa/PRoot runtime, root filesystem, or game launcher bridge. The app intentionally does not pretend that imported `.exe` files can run.

The next engineering step is to port the upstream Winlator application/runtime and its native assets into a properly licensed build, then connect PROJECT R's library and game profiles to the runtime's container/shortcut APIs.

## Upstream engine research

- Winlator source: https://github.com/brunodev85/winlator
- Winlator app source: https://github.com/brunodev85/winlator-app
- Winlator documentation and release notes: https://github.com/brunodev85/winlator#readme

Winlator depends on a coordinated set of components, including Wine, Box86/Box64, Mesa graphics components, PRoot/root filesystem assets and audio/input integration. These are not interchangeable single Android dependencies. Use the upstream source and its current submodules/build scripts rather than copying arbitrary prebuilt binaries.

### Redmi K50i target

The target device is a MediaTek Dimensity 8100 phone with a Mali GPU. Do not select Adreno-only Turnip drivers for this device. Runtime integration must detect supported Vulkan/OpenGL capabilities and select a backend that is actually compatible with the GPU. Mali performance/compatibility must be validated on-device; no working game execution is claimed yet.

## Build

Requirements:
- JDK 17
- Android SDK 35
- Android Gradle Plugin 8.7.3
- Kotlin 2.0.21

Build command:

```bash
gradle --no-daemon assembleDebug
```

APK output:

```text
app/build/outputs/apk/debug/app-debug.apk
```

## GitHub Actions

The included workflow supports either:
1. Gradle project files at repository root; or
2. The complete `project_r/` folder at repository root.

Run **Actions → Build PROJECT R APK → Run workflow**.

## Licensing

PROJECT R's original launcher code is provided for this personal project. No Winlator source code or third-party runtime binaries are bundled in this phase. When upstream code or components are integrated, preserve their respective copyright notices, licence texts, source-offer/source-disclosure requirements and third-party notices. Review the exact licence files of the specific upstream revision and each dependency before distributing any build.

## Phase roadmap

- Phase 1: Android launcher foundation — completed and installed by user.
- Phase 2: Premium UI refresh + runtime integration preparation — this package.
- Phase 3: Port Winlator runtime and connect container lifecycle.
- Phase 4: Game executable detection, profiles and launch flow.
- Phase 5: GPU/backend tuning and performance telemetry.
- Phase 6: Touch controls, controller support and IGI 2 testing.
