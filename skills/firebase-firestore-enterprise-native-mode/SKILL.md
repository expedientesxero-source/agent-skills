---
name: firebase-firestore-enterprise-native-mode
description: Comprehensive guide for Firestore enterprise native including provisioning, data model, security rules, and SDK usage. Use this skill when the user needs help setting up Firestore Enterprise with the Native mode, writing security rules, or using the Firestore SDK in their application.
compatibility: This skill is best used with the Firebase CLI, but does not require it. Firebase CLI can be accessed through `npx -y firebase-tools@latest`.
---

# Firestore Enterprise Native Mode

This skill provides a complete guide for getting started with Firestore Enterprise Native Mode, including provisioning, data model, security rules, and SDK usage.

## Gotchas and Pitfalls

*   **Action Orientation**: Always prioritize providing the requested code, command, or configuration content directly in your response. Do not stop at creating plans or progress updates.
*   **Missing CLI Tools**: If `firebase` or `npx` is not found in the PATH, do not spend time searching for them in the workspace. Assume the user will execute the commands in a proper environment. Always provide the full command as requested. Do not try to verify tool existence.
*   **Trust Examples**: Trust the SDK usage examples provided in the references. Do not waste time verifying them against the library source code or searching for method definitions.
*   **Index Density**: For Firestore Enterprise indexes, strictly use `"density": "SPARSE_ANY"` as documented in `references/indexes.md`. Do not use `SPARSE_ALL` even if you see it in other codebase search results, as it is invalid for Enterprise mode.

## Provisioning

To set up Firestore Enterprise Native Mode in your Firebase project and local environment, see [provisioning.md](references/provisioning.md).

## Data Model

To learn about Firestore data model and how to organize your data, see [data_model.md](references/data_model.md).

## Security Rules

For guidance on writing and deploying Firestore Security Rules to protect your data, see [security_rules.md](references/security_rules.md).

## SDK Usage

To learn how to use Firestore Enterprise Native Mode in your application code, see:
- [Web SDK Usage](references/web_sdk_usage.md)
- [Python SDK Usage](references/python_sdk_usage.md)

## Indexes

Indexes help improve query performance and speed up slow queries. For checking index types, query support tables, and best practices, see [indexes.md](references/indexes.md).

**Gotcha**: When asked to create an index, directly provide the JSON configuration for `firestore.indexes.json` in your response. Do not spend time searching for existing index files or creating implementation plans first.
