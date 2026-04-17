---
name: firebase-unity-basic
description: >-
  Provides foundational setup and initialization for Firebase in Unity, including FirebaseApp, Auth, and Firestore. Use when setting up Firebase in a Unity project, initializing FirebaseApp, or creating instances of Auth and Firestore in Unity.
---

# Prerequisites

Before using Firebase in Unity, ensure you have: 1. Imported the Firebase Unity
SDK (.unitypackage files) into your project. 2. Configured your Unity project
for the target platform (Android/iOS/Desktop). 3. Added the
`google-services.json` (Android) or `GoogleService-Info.plist` (iOS) to your
project.

# Firebase Unity Basics

## 1. Initializing Firebase App

Before calling any Firebase methods, you must verify that the required Google
Play services are available on the device and are up to date.

```csharp
using Firebase;
using Firebase.Extensions;
using UnityEngine;

public class FirebaseInit : MonoBehaviour
{
    void Start()
    {
        FirebaseApp.CheckAndFixDependenciesAsync().ContinueWithOnMainThread(task => {
            var dependencyStatus = task.Result;
            if (dependencyStatus == DependencyStatus.Available) {
                // Create and hold a reference to your FirebaseApp,
                // where app is a Firebase.FirebaseApp property of your application class.
                FirebaseApp app = FirebaseApp.DefaultInstance;

                // Set a flag here to indicate whether Firebase is ready to use by your app.
                Debug.Log("Firebase is ready!");
            } else {
                Debug.LogError(System.String.Format(
                  "Could not resolve all Firebase dependencies: {0}", dependencyStatus));
                // Firebase Unity SDK is not safe to use here.
            }
        });
    }
}
```

## 2. Getting Auth Instance

Once `FirebaseApp` is initialized, you can get the `FirebaseAuth` instance.

```csharp
using Firebase.Auth;

// Get the default auth instance
FirebaseAuth auth = FirebaseAuth.DefaultInstance;
```

## 3. Getting Firestore Instance

Similarly, you can get the `FirebaseFirestore` instance.

```csharp
using Firebase.Firestore;

// Get the default firestore instance
FirebaseFirestore db = FirebaseFirestore.DefaultInstance;
```

# Gotchas

-   **Always** check dependencies using `CheckAndFixDependenciesAsync()` before
    using any Firebase features. Failing to do so may result in crashes on
    Android devices without Google Play Services.
-   **ContinueWithOnMainThread**: Always use `ContinueWithOnMainThread` when
    handling tasks from Firebase async methods if you need to interact with
    Unity objects or run code on the main thread.
