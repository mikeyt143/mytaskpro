## Goal

Integrate the upstream `tasks/tasks` Android project into this workspace so you can base your app build on it, while complying with the GNU GPL v3 license.

## Checklist (requirements extracted)
- Clone or add the upstream project into the workspace (done: cloned to `third_party/tasks`).
- Decide integration method (fork+submodule recommended) and implement.
- Ensure GPLv3 compliance when distributing (include license, make source available, display legal notices).
- Provide build environment and commands for local and CI builds.

## Actions already performed
- Cloned upstream `https://github.com/tasks/tasks.git` into `third_party/tasks`.
- Read `README.md` and `LICENSE` (GNU GPL v3).

## Assumptions
- You will distribute the final app (APK/AAB) or modified code. If you only use it privately, GPL obligations differ.
- Android build environment (JDK, Android SDK) is not yet installed in this dev container.

## Recommended integration options
1) Fork upstream and use a git submodule (recommended for working with upstream changes and clean attribution).
   - Benefits: easy to pull upstream updates, clear boundary between your code and upstream.
2) Vendor the code into `third_party/tasks` (already done by cloning).
   - Benefits: simple, but you must maintain updates manually and include full source when distributing.
3) Re-implement features and keep only small copied pieces (risky legally — if pieces create a derivative work, GPL may still apply).

If you want a clean workflow, I recommend: fork -> add upstream remote -> add as a submodule in this repo.

## Quick commands

Clone (if you prefer a submodule instead of the existing clone):
```bash
# From repo root
git submodule add https://github.com/tasks/tasks.git third_party/tasks
git submodule update --init --recursive
```

Build (on a machine with Android SDK + JDK installed):
```bash
# From third_party/tasks
./gradlew assembleDebug
# or build a release bundle
./gradlew bundleRelease
```

Replace the existing clone with a submodule (if you choose to):
```bash
# remove the current cloned folder (ensure you have no local changes you need)
rm -rf third_party/tasks
git add -A
git commit -m "Remove vendor copy to replace with submodule"
git submodule add https://github.com/tasks/tasks.git third_party/tasks
git commit -m "Add tasks upstream as submodule"
```

## GPL v3 compliance (practical checklist)
- Keep the upstream `LICENSE` file and any copyright notices in the source tree you distribute.
- If you distribute the binary (APK/AAB), you must also make the corresponding source available under GPLv3.
  - Practical: provide a link in your app's Play Store listing or in-distribution files to a public repository (your fork) containing the full source and build instructions.
- Mark modifications clearly and include relevant dates (see GPL section 5a).
- If the app has interactive UI, include "Appropriate Legal Notices" in an About screen (copyright, license, and how to get source).

## Development notes and hazards
- Upstream uses Gradle / Android; match the JDK and Gradle versions referenced in `gradle.properties` and `gradle/wrapper`.
- When pulling upstream changes, re-run Gradle sync and run tests.
- Keep proprietary code separate; if combined with GPL code into one work, the whole combined work must be licensed under GPLv3.

## Next recommended steps I can do for you
1. Convert the current clone into a git submodule (or remove it and add submodule) — I can perform this if you want.
2. Create a fork of the upstream repo under your GitHub account and set it as the submodule target.
3. Add an "About" screen stub to the app to display license + source URL (small code change).

Tell me which of the three next steps you want me to execute and I will do it now.

---
File created by automation: summary of integration actions and next steps.
