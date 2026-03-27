# Firebase iOS Setup Guide

## 1. Create a Firebase Project and App (Automated)
Do not use the Firebase Console. Use the CLI to automate setup:

1. Create the project: `npx -y firebase-tools@latest projects:create`
2. Register the iOS app: `npx -y firebase-tools@latest apps:create IOS <bundle-id>`
3. Fetch the config: `npx -y firebase-tools@latest apps:sdkconfig IOS <App-ID>`
4. Save the output as `GoogleService-Info.plist` in your Xcode project folder. Ensure you remove any non-XML CLI output headers.

## 2. Installation (Automated via Swift Package Manager CLI)
Do not use raw text parsing, sed, or Ruby scripts (like `xcodeproj` gem) to modify `.pbxproj` files directly.

Instead, use the **`xcode-project-setup`** skill. 
Load that skill using your tools to securely execute its native Swift package setup script. That skill handles installing the required SPM packages and safely linking the `GoogleService-Info.plist` file.

## 3. Initialization
Configure the shared `FirebaseApp` instance. You can do this either in a modern SwiftUI `App` structure or a traditional `AppDelegate`.

### SwiftUI (Modern)
```swift
import SwiftUI
import FirebaseCore

@main
struct YourApp: App {
  init() {
    FirebaseApp.configure()
  }

  var body: some Scene {
    WindowGroup {
      ContentView()
    }
  }
}
```
> **⚠️ CRITICAL SWIFTUI INITIALIZATION WARNING:**
> Never initialize Firebase-dependent objects (like an `AuthViewModel` or `Firestore` service) using `@State`, `@StateObject`, or global variables at the root `App` struct level. Property initializers run *before* the `init()` method where `FirebaseApp.configure()` is called, causing an immediate fatal crash. 
> Always instantiate these view models further down the view hierarchy (e.g., inside `ContentView`).

### AppDelegate (Traditional / UIKit)
```swift
import UIKit
import FirebaseCore

@main
class AppDelegate: UIResponder, UIApplicationDelegate {
  func application(_ application: UIApplication,
                   didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey : Any]? = nil) -> Bool {
    FirebaseApp.configure()
    return true
  }
}
```
