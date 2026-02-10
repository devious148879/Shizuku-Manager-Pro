# CLAUDE.md — AI Assistant Guide for Shizuku Manager Pro

This file provides context for AI assistants (Claude Code, etc.) working in this repository.

## Project Overview

**Shizuku Manager Pro** (also called **Privilege Manager Pro**) is a native Android application for ADB-based privilege management. It allows power users to execute privileged shell commands without root access, using Shizuku/ADB as the privilege elevation mechanism.

- **Language**: Kotlin
- **UI Framework**: Jetpack Compose with Material Design 3
- **Min SDK**: Android API 34
- **Build System**: Gradle (Kotlin DSL — `build.gradle.kts`)
- **Package name**: `com.privilegemanager.pro`

## Repository Status

This repository is in an **early/documentation stage**. The README describes the full intended architecture and feature set, but the Kotlin source files, Gradle build scripts, and Android manifests have not yet been committed. The only tracked file is `README.md`.

When source code is added, it will follow the structure documented below.

## Intended Project Structure

```
app/src/main/java/com/privilegemanager/pro/
├── MainActivity.kt              # App entry point (single Activity)
├── data/
│   ├── DataModels.kt            # Data classes: Shortcut, Template, etc.
│   └── DataStore.kt             # Persistence via Jetpack DataStore
├── service/
│   └── ShellExecutor.kt         # Command execution engine (ADB/Shizuku)
├── ui/
│   ├── screens/
│   │   ├── MainScreen.kt        # Top-level navigation & tab layout
│   │   ├── HomeScreen.kt        # Service start/stop controls
│   │   ├── ShortcutsScreen.kt   # Custom shortcut management
│   │   ├── TemplatesScreen.kt   # Reusable command templates
│   │   ├── ExecutorScreen.kt    # Free-form command executor
│   │   └── APIReferenceScreen.kt # 59+ pre-configured ADB commands
│   └── theme/
│       ├── Color.kt             # Color definitions
│       ├── Theme.kt             # Material 3 theme setup
│       └── Type.kt              # Typography
└── viewmodel/
    └── AppViewModel.kt          # Central state management (ViewModel)
```

## Architecture & Patterns

- **Single Activity** architecture — `MainActivity.kt` hosts all Compose screens
- **MVVM** — `AppViewModel` holds app state; screens observe via Compose state
- **Jetpack DataStore** for persistence (not Room/SQLite)
- **Gson** for JSON serialization (export/import)
- **Coroutines** for async operations (shell execution, I/O)
- **State hoisting** — screens receive state from the ViewModel, callbacks flow up

## Build & Run Commands

```bash
# Build debug APK
./gradlew assembleDebug

# Build release APK
./gradlew assembleRelease

# Install debug build to connected device
./gradlew installDebug

# Clean build artifacts
./gradlew clean

# Refresh dependencies
./gradlew --refresh-dependencies

# Launch app via ADB
adb shell am start -n com.privilegemanager.pro/.MainActivity
```

Output locations:
- Debug APK: `app/build/outputs/apk/debug/app-debug.apk`
- Release APK: `app/build/outputs/apk/release/app-release-unsigned.apk`

## Key Dependencies

| Library | Purpose |
|---------|---------|
| `androidx.compose:compose-bom:2023.10.01` | Compose version alignment |
| `androidx.compose.material3:material3` | Material 3 UI components |
| `androidx.compose.material:material-icons-extended` | Extended icon set |
| `androidx.lifecycle:lifecycle-viewmodel-compose` | ViewModel integration |
| `androidx.datastore:datastore-preferences` | Local key-value persistence |
| `com.google.code.gson:gson` | JSON serialization |
| `dev.rikka.shizuku:api:13.1.5` | Shizuku privilege API (optional) |

## Prerequisites

- **Android Studio** Hedgehog (2023.1.1) or newer
- **JDK 17+**
- **Android SDK** API 34
- **Kotlin** 1.9.0+

## Coding Conventions

- Follow standard **Kotlin coding conventions** (kotlinlang.org style guide)
- Compose screens are `@Composable` functions, one primary screen per file
- Use `remember` and `derivedStateOf` for expensive computations in Compose
- Prefer `LazyColumn`/`LazyRow` over `Column`/`Row` for scrollable lists
- Coroutine scopes come from `viewModelScope` — avoid `GlobalScope`
- Variable/function naming: `camelCase`; classes: `PascalCase`
- Format code with Android Studio's default formatter

## Security Considerations

This app executes shell commands with elevated privileges. When contributing:

- **Never** hardcode credentials, API keys, or tokens
- **Never** commit keystores or signing configs
- Review all shell command strings for injection risks
- Validate and sanitize user input before passing to `ShellExecutor`
- Commands run with ADB/Shizuku privilege — treat them like root commands
- Do not add network call capabilities that could exfiltrate data

## Git Workflow

- **Default branch**: `master`
- **Feature branches**: `feature/<name>` or `claude/<description>-<id>`
- Write clear, concise commit messages (imperative mood)
- No force-pushing to `master`
- PRs should describe what changed and why

## What's Not in the Repo Yet

The following items are described in the README but not yet checked in:
- All Kotlin source files (`*.kt`)
- Gradle build scripts (`build.gradle.kts`, `settings.gradle.kts`)
- Android Manifest (`AndroidManifest.xml`)
- Resource files (`res/xml/file_paths.xml`, themes, etc.)
- Gradle wrapper (`gradlew`, `gradle/`)

When these are added, this file should be updated to reflect actual (not just planned) structure.

## Roadmap Context

- **v1.0.0** (current target): Core features — service management, shortcuts, templates, executor, API reference, data persistence
- **v1.1.0**: Import backups, command history, favorites, scheduled commands, dark/light theme
- **v1.2.0**: Widgets, Tasker integration, multi-command execution, advanced logging
- **v2.0.0**: Plugin system, community templates, script editor, cloud sync
