# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

GKD is an Android Accessibility Tool that provides custom screen clicking automation using:
- **Advanced Selectors** - CSS-like selectors for UI element targeting
- **Subscription Rules** - Remote rule management capabilities
- **Snapshot Review** - UI element inspection and debugging

This is a sophisticated Android accessibility service that automates screen interactions through a rule-based system.

## Architecture

**Multi-module Android project**:
- **:app** - Main application module (primary focus)
- **:selector** - KMP module for selector engine (JVM + JS targets)
- **:hidden_api** - Android library for hidden API access

**Key architectural patterns**:
- **MVVM pattern** with ViewModels and Jetpack Compose UI
- **Repository pattern** for data management
- **Service-based architecture** with 9 different Android services
- **Room database** for local data persistence
- **Event-driven design** for accessibility event processing

## Technology Stack

- **Language**: Kotlin (100%)
- **UI Framework**: Jetpack Compose
- **Build System**: Gradle with Kotlin DSL
- **Database**: Room
- **Async**: Kotlin Coroutines
- **HTTP Client**: Ktor
- **Navigation**: Compose Destinations
- **Image Loading**: Coil

## Development Commands

### Building and Running
```bash
./gradlew build                    # Build the project
./gradlew assembleDebug           # Build debug variant
./gradlew assembleRelease         # Build release variant
./gradlew installDebug            # Install debug build to device
./gradlew test                    # Run tests
```

### Build Variants
- **gkd**: Default channel (accessibility tool enabled)
- **play**: Google Play store channel (accessibility disabled)

### Testing
```bash
./gradlew test                    # Run unit tests
./gradlew connectedAndroidTest    # Run instrumented tests
```

## Key Components and Directories

### Core App Structure (`app/src/main/kotlin/li/songe/gkd/`)
- **a11y/** - Accessibility service logic and event handling
- **data/** - Data models and entities
- **db/** - Room database configuration and DAOs
- **permission/** - Permission management system
- **service/** - Android services (9 different services)
- **shizuku/** - Shizuku integration for system-level access
- **store/** - State management
- **ui/** - Compose UI components and screens

### Services
The app uses 9 different Android services for various functionalities including accessibility service, foreground services, and background processing.

## Development Setup

### Requirements
- Android SDK API 26-36 (Android 8.0 - 14)
- Latest Android Studio with Kotlin support
- Physical Android device or emulator for testing

### Permissions Required
Key permissions that need to be granted during development:
- `android.permission.SYSTEM_ALERT_WINDOW` - Overlay windows
- `android.permission.QUERY_ALL_PACKAGES` - App discovery
- `android.permission.WRITE_SECURE_SETTINGS` - System settings

## Important Notes

### Accessibility Service
The core functionality depends on being an accessibility service. During development, ensure accessibility permissions are properly configured and tested.

### Selector Engine
The selector engine uses CSS-like syntax to target UI elements. When working with selectors, understand the advanced selector system described in the project documentation.

### Subscription System
GKD supports remote rule subscriptions via HTTP. The app doesn't provide default rules - they must be added locally or via subscriptions.

### Build Configuration
- Uses custom signing configurations for different build variants
- Includes ProGuard/R8 optimization for release builds
- Supports both debug and release signing setups
- Git integration for automatic versioning

### Platform-Specific Features
- **Shizuku Integration**: For elevated system permissions without root
- **Quick Settings Tiles**: Multiple Android Quick Settings integration
- **HTTP Server**: Internal server for external communication
- **Snapshot Tool**: For UI element inspection and rule debugging