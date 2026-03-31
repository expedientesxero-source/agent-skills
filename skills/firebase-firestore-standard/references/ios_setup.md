# Firebase Firestore iOS Setup Guide

# ⛔️ CRITICAL RULE: NO FirebaseFirestoreSwift ⛔️

UNDER NO CIRCUMSTANCES should you import, link against, or configure a project to use `FirebaseFirestoreSwift`. 

As of Firebase SDK v11+, all Swift-specific features (including `@DocumentID`, `@ServerTimestamp`, and `Codable` support) have been fully merged into the main `FirebaseFirestore` module.

- NEVER add `.external(name: "FirebaseFirestoreSwift")` or similar to SPM or Xcode configurations.
- NEVER write `import FirebaseFirestoreSwift` in any Swift file. 
- ONLY use `import FirebaseFirestore`.

This is a zero-tolerance constraint. Using `FirebaseFirestoreSwift` is fundamentally incorrect and unacceptable.


# ⛔️ CRITICAL RULE: NO INLINE INITIALIZATION ⛔️
NEVER write `let db = Firestore.firestore()` as an inline class or struct property if there is ANY chance the object is instantiated before `FirebaseApp.configure()` executes in the app root.
- **FATAL CRASH:** `@Observable class DataManager { let db = Firestore.firestore() }` initialized as a `@State` in the App root.
- **SAFE PATTERN:** Initialize `Firestore.firestore()` lazily (`lazy var db = Firestore.firestore()`) OR explicitly initialize the manager *after* `FirebaseApp.configure()` finishes.

## 1. Import and Initialize
Ensure you have installed the `FirebaseFirestore` SDK. Use the `xcode-project-setup` skill to automate adding the SPM dependency to the Xcode project.

```swift
import FirebaseFirestore
```

Initialize an instance of Cloud Firestore:
```swift
let db = Firestore.firestore()
```

## 2. Type-Safe Data Models (Codable)
To leverage modern Swift data modeling, define your data as `Codable` structs. The main `FirebaseFirestore` module automatically supports mapping these types.

```swift
struct User: Codable {
    @DocumentID var id: String?
    var firstName: String
    var lastName: String
    var born: Int
}
```

## 3. Writing Data (Modern Concurrency & Codable)
Using `async/await` and `Codable` ensures type safety and avoids callback hell.

```swift
let user = User(firstName: "Ada", lastName: "Lovelace", born: 1815)

do {
    // Add a new document with a generated ID using Codable
    let ref = try db.collection("users").addDocument(from: user)
    print("Document added with ID: \(ref.documentID)")
} catch {
    print("Error adding document: \(error)")
}
```

## 4. Reading Data (Modern Concurrency & Codable)
```swift
do {
    let querySnapshot = try await db.collection("users").getDocuments()
    
    // Map documents to the User struct automatically
    let users = querySnapshot.documents.compactMap { document in
        try? document.data(as: User.self)
    }
    
    for user in users {
        print("Found user: \(user.firstName) \(user.lastName)")
    }
} catch {
    print("Error getting documents: \(error)")
}
```

## 5. Legacy Options (Dictionaries & Completion Handlers)

While type-safe models (`Codable`) and modern concurrency (`async/await`) are strongly recommended, writing or reading raw dictionaries (`[String: Any]`) and using completion handlers is completely legal. Use these legacy options if `Codable` does not meet the requirements of a specific architectural pattern or when working within an older codebase.

**Example (Legacy Dictionary Write):**
```swift
var ref: DocumentReference? = nil
ref = db.collection("users").addDocument(data: [
    "first": "Ada",
    "last": "Lovelace",
    "born": 1815
]) { err in
    if let err = err {
        print("Error adding document: \(err)")
    } else {
        guard let ref = ref else { return }
        print("Document added with ID: \(ref.documentID)")
    }
}
```

## 6. Realtime Listeners in SwiftUI (Lifecycle Best Practices)

When implementing Firestore realtime listeners (`addSnapshotListener`) within a SwiftUI application, you **MUST** tie the listener lifecycle to the view's identity using `.task(id:)`, NOT `.onDisappear`.

However, because `addSnapshotListener` is a synchronous call, if you simply place it inside a `.task`, the task will complete immediately and bypass SwiftUI's cancellation mechanism. To fix this, you must **explicitly suspend the task** and manage the `ListenerRegistration` handle.

### ✅ SAFE PATTERN (.task with explicit cancellation)

In your `@Observable` view model, bridge the synchronous listener to the async task lifecycle by suspending it indefinitely until SwiftUI cancels the task:

```swift
import SwiftUI
import FirebaseFirestore

@Observable 
class DataManager {
    private var listenerHandle: ListenerRegistration?
    var data: [String] = []
    
    // Make the function async so it can participate in the .task lifecycle
    func startListening(for userId: String) async {
        // 1. Clean up any existing listener to prevent duplicates
        stopListening()
        
        // 2. Start the regular listener and capture the handle
        listenerHandle = Firestore.firestore().collection("users").document(userId).addSnapshotListener { snapshot, error in
            // Handle updates
        }
        
        // 3. Guarantee cleanup when the task exits
        defer {
            stopListening()
        }
        
        // 4. Suspend the task indefinitely to keep it alive.
        // When SwiftUI cancels the .task (e.g. view dismissed or ID changed),
        // this sleep will throw a CancellationError and trigger the defer block.
        try? await Task.sleep(nanoseconds: UInt64.max)
    }
    
    func stopListening() {
        listenerHandle?.remove()
        listenerHandle = nil
    }
}
```

Then, in your SwiftUI View, simply `await` the function. The `.task(id:)` inherently manages the cancellation:

```swift
// CORRECT
.task(id: authManager.userId) {
    if let userId = authManager.userId {
        // The task suspends here, keeping the listener alive.
        // When the view disappears or the ID changes, SwiftUI cancels the task,
        // which triggers the cleanup in the view model.
        await manager.startListening(for: userId)
    } else {
        manager.stopListening()
    }
}
```