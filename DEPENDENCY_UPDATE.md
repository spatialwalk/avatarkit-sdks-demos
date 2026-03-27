# Demo Dependency Update Workflow

After every SDK release, update the corresponding demo project to use the new SDK version.

## Web Demos

**Version file:** each sub-project's `package.json` → `dependencies["@spatialwalk/avatarkit"]`

| Sub-project | Path |
|-------------|------|
| React | `web/react/package.json` |
| Vue | `web/vue/package.json` |
| Vanilla | `web/vanilla/package.json` |
| Next.js Direct | `web/nextjs-direct/package.json` |
| Next.js iframe | `web/nextjs-iframe/iframe-content/package.json` |

**Steps:**

1. Bump `@spatialwalk/avatarkit` version in all 5 `package.json` files
2. Run `pnpm install` (or `npm install`) in each sub-project to verify resolution
3. Build and smoke-test at least one demo (e.g. `react`) to confirm no API breaks
4. Update `web/README.md` if it mentions a specific SDK version

## Android Demo

**Version file:** `android/gradle/libs.versions.toml` → `avatarKit` field under `[versions]`

**Steps:**

1. Bump the `avatarKit` version in `libs.versions.toml`
2. Sync Gradle to verify dependency resolution
3. Build and run the demo to confirm no API breaks

## iOS Demo

**Version file:** `ios/AvatarKitExample/AvatarKit.xcframework` (bundled binary)

The iOS demo embeds `AvatarKit.xcframework` directly — there is no package manager.

**Download URL:** check `ios-sdk/README.md` → Installation section for the latest COS URL, format:
```
https://character-resource-bj-1373098193.cos.ap-beijing.myqcloud.com/xcframework/AvatarKit_<YYYYMMDDHHMM>.zip
```

**Steps:**

1. Download the new `AvatarKit.xcframework` zip from the COS URL in `ios-sdk/README.md`
2. Unzip and replace `ios/AvatarKitExample/AvatarKit.xcframework` with the new version
3. Open `ios/Example.xcworkspace` in Xcode, build and run to confirm no API breaks

## Flutter Demo (if exists)

**Version file:** `flutter/pubspec.yaml` → `avatar_kit`

**Steps:**

1. Bump `avatar_kit` version in `pubspec.yaml`
2. Run `flutter pub get` to verify resolution
3. Build and run the demo to confirm no API breaks

## Final Steps

1. Commit and push all demo dependency changes
2. Verify demos in CI (if applicable)
