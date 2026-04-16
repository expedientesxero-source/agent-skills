# Firebase Crashlytics iOS Setup Guide

Important references:

- Refer to the `firebase-basics` skills, particularly those for iOS setup, before proceeding.
- Refer to the `xcode-project-setup` skills.

## 1. Automated Project and App Setup

Use the `firebase-tools` CLI to set up the project if necessary.

1.  **Find Bundle ID:** Read the Xcode project to find the iOS bundle ID. Check the `PRODUCT_BUNDLE_IDENTIFIER` value in the `.pbxproj` file or the `Info.plist` file.
2.  **Create Firebase Project:** If no project exists, create one:
    `npx -y firebase-tools@latest projects:create <project-id> --display-name="My Awesome App"`
3.  **Create Firebase App:** Register the iOS app with the discovered bundle ID:
    `npx -y firebase-tools@latest apps:create IOS <bundle-id>`
4.  **Link the GoogleService-Info.plist file:** Use the script in the `xcode-project-setup` skill to obtain the config and link.

## 2. Add Swift Package Dependencies

Install the SDK using the Swift packages manager, or the script in the `xcode-project-setup` skill.

The following packages are required from the `https://github.com/firebase/firebase-ios-sdk.git` repository:
- `FirebaseCrashlytics`
- `FirebaseAnalytics`

## 3. Initialize Firebase in App Code

Modify the application's entry point to initialize Firebase. Refer to the iOS setup reference in the `firebase-basics` skill.

## 4. Add dSYM Upload Script

Add a Run Script phase to the main app target in Xcode. This step is required to upload dSYM files for crash symbolication. 

1.  **Debug Information Format**: The `Debug Information Format` in Build Settings must be set to `DWARF with dSYM File`.
2.  **Run Script Content**: A new "Run Script Phase" should be added to the target's "Build Phases" with the following content:
    ```bash
    ${BUILD_DIR%/Build/*}/SourcePackages/checkouts/firebase-ios-sdk/Crashlytics/run
    ```

## 5. Force a Test Crash

**Action:** Add code to trigger a crash a few seconds after app startup to verify Crashlytics setup.

1.  **For SwiftUI Apps (in `AppDelegate.swift`):**

    *File: `AppDelegate.swift`*
    ```swift
    import FirebaseCore
    import Dispatch // For DispatchQueue

    // ...

    class AppDelegate: NSObject, UIApplicationDelegate {
      func application(_ application: UIApplication,
                       didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]? = nil) -> Bool {
        FirebaseApp.configure()
        // Force a crash after a delay to test Crashlytics
        DispatchQueue.main.asyncAfter(deadline: .now() + 3) {
            fatalError("Test Crash")
        }
        return true
      }
    }
    ```

After adding the code, build and run your app. It should crash after approximately 3 seconds. Restart the app. The Crashlytics SDK will send the crash report to Firebase on the next app launch. The report will appear in the Firebase console after a few minutes.
