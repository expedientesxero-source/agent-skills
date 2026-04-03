---
name: eject-extension
description: Skill for moving extensions code from being managed by Extensions to being local functions code
---

# Extension to Functions Codebase

## Overview

A user wants to fork their extension and make it a local codebase. This will download
the extensions code, convert it to v2 functions code, copy all the local parameters,
and then manage deleting the extension and deploying the function

## Triggers
Activate this skill when a developer expresses that they wish to make their extension
locally managed.

## Follow up
If there are any tests in the extensions codebase, be sure to run them after the migration.

## Steps

### Copy the extension to a local directory
Find which extension the user is referring to and find out about it with `firebase ext:list --json` in the current project.
This will provide you with all instances of the extension in the customer's project as well as their parameters.
REMEMBER these parameters' values. You will need to re-enter them when you create the new functions codebase.

### Download the extensions locally
Use the `firebase ext:info` command to print out information about the extension and get the download URL for its source.
Create a directory inside the customer's project named after the extension. Download and unzip the extensions' source
into that directory.

### Upgrade the code to Functions code
Use the extensions-to-functions-codebase skill to convert the extensions code to Firebase Functions code in place. Run tests
if available.

### Upgrade the functions from V1 to V2
Use the skill at https://github.com/firebase/agent-skills/pull/60 to upgrade the functions from V1 to V2.

### Copy over the extensions' configuration
For each extension instance that the user had, create a new folder to hold its config. The config you downloaded earlier
should become part of .env files (unless there are secrets, they should just automatically be picked up with Cloud Secrets Manager).

Next, update firebase.json to create the codebase. The codebase should be [extension]-[instance] with the source directory as
the directory with the source and the configDir as the directory with the .env files. The codebase should have the instance as a prefix.

### Copy over local extensions' configuration
If the extension is defined in firebase.json as a local install for local environment variables, save those values in the codebase for
that extension instance as .env.local.
