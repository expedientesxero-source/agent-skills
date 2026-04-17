# Firebase Unity Basic Skill - Agent E2E Test Plan

## Prerequisites

**Read `SKILL.md` first** to understand available code snippets and expected behavior.

This skill provides code snippets and guidelines for using Firebase in Unity. There is no CLI binary to build.

---

## Test 1: Initialize Firebase in Unity

**Prompt:** "I want to use Firebase in my Unity game. How do I set it up in a script so it's safe to use?"

**Verify:**
- The agent provides a C# code snippet.
- The snippet uses `FirebaseApp.CheckAndFixDependenciesAsync()`.
- The snippet handles the result and checks for `DependencyStatus.Available`.

---

## Test 2: Get Auth and Firestore Instances

**Prompt:** "Show me how to access Firebase Auth and Firestore in my Unity code after I've initialized the app."

**Verify:**
- The agent provides code snippets for both Auth and Firestore.
- The snippet uses `FirebaseAuth.DefaultInstance`.
- The snippet uses `FirebaseFirestore.DefaultInstance`.
