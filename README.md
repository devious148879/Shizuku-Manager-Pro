# Privilege Manager Pro - Android Native App

A powerful Android privilege elevation tool built with Kotlin and Jetpack Compose, converted from the React web prototype.

---

## 📱 About

**Privilege Manager Pro** is a comprehensive ADB-based privilege management application that allows Android power users to execute privileged commands without root access. It features custom shortcuts, reusable templates, and an extensive API reference with 59+ pre-configured commands.

---

## ✨ Features

### Core Functionality
- ✅ **Service Management** - Start/stop privilege service via Wireless ADB, USB, or Root
- ✅ **Command Execution** - Execute shell commands with elevated privileges
- ✅ **Real-time Status** - Monitor service status and activity logs
- ✅ **Advanced Settings** - Auto-start, notifications, debug mode, wake lock

### Custom Shortcuts (Tab 1)
- ✅ Create shortcuts with custom names, emojis, and commands
- ✅ Categorize shortcuts (Package, System, Network, Custom)
- ✅ One-tap execution
- ✅ Grid view with hover actions
- ✅ Delete shortcuts

### Command Templates (Tab 2)
- ✅ Reusable command patterns with placeholders
- ✅ Star favorite templates
- ✅ Placeholder detection (`{package}`, `{permission}`, etc.)
- ✅ Direct executor integration
- ✅ 6 pre-configured templates

### Command Executor (Tab 3)
- ✅ Multi-line command input
- ✅ Real-time output display
- ✅ Quick command buttons
- ✅ Service status validation
- ✅ Copy/clear output
- ✅ Placeholder warnings

### API Reference (Tab 4)
- ✅ 7 categories with 59+ commands
- ✅ Real-time search filtering
- ✅ One-click execute or copy
- ✅ Expandable categories
- ✅ Detailed command descriptions

### Data Management
- ✅ DataStore persistence
- ✅ Export to JSON
- ✅ Automatic data saving
- ✅ State preservation

---

## 🏗️ Project Structure

```
app/src/main/java/com/privilegemanager/pro/
├── MainActivity.kt                    # App entry point
├── data/
│   ├── DataModels.kt                 # Data classes (Shortcut, Template, etc.)
│   └── DataStore.kt                  # Persistence layer
├── service/
│   └── ShellExecutor.kt              # Command execution engine
├── ui/
│   ├── screens/
│   │   ├── MainScreen.kt             # Navigation & layout
│   │   ├── HomeScreen.kt             # Service control
│   │   ├── ShortcutsScreen.kt        # Shortcuts management
│   │   ├── TemplatesScreen.kt        # Templates management
│   │   ├── ExecutorScreen.kt         # Command executor
│   │   └── APIReferenceScreen.kt     # API reference
│   └── theme/
│       ├── Color.kt                  # Color definitions
│       ├── Theme.kt                  # Material 3 theme
│       └── Type.kt                   # Typography
└── viewmodel/
    └── AppViewModel.kt               # State management
```

---

## 🚀 Getting Started

### Prerequisites
- **Android Studio** Hedgehog (2023.1.1) or newer
- **JDK 17** or higher
- **Android SDK** with API 34
- **Kotlin** 1.9.0+

### Installation Steps

1. **Clone or Create Project**
   ```bash
   # In Android Studio: File > New > New Project
   # Select "Empty Activity" (Compose)
   # Package: com.privilegemanager.pro
   # Language: Kotlin
   # Minimum SDK: API 26
   ```

2. **Copy All Files**
   - Copy all provided `.kt` files to their respective packages
   - Update `build.gradle.kts` with dependencies
   - Update `AndroidManifest.xml`
   - Create `res/xml/file_paths.xml`

3. **Sync Gradle**
   ```bash
   ./gradlew sync
   ```

4. **Build Project**
   ```bash
   ./gradlew assembleDebug
   ```

5. **Run on Device**
   - Connect Android device via USB
   - Enable USB Debugging
   - Click Run (Shift + F10)

---

## 📦 Dependencies

```kotlin
// Core
implementation("androidx.core:core-ktx:1.12.0")
implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.6.2")
implementation("androidx.activity:activity-compose:1.8.1")

// Compose
implementation(platform("androidx.compose:compose-bom:2023.10.01"))
implementation("androidx.compose.ui:ui")
implementation("androidx.compose.material3:material3")
implementation("androidx.compose.material:material-icons-extended")

// ViewModel
implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.6.2")

// DataStore
implementation("androidx.datastore:datastore-preferences:1.0.0")

// JSON
implementation("com.google.code.gson:gson:2.10.1")

// Shizuku (Optional)
implementation("dev.rikka.shizuku:api:13.1.5")
```

---

## 🔧 Configuration

### AndroidManifest.xml Permissions
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="moe.shizuku.manager.permission.API_V23" />
```

### File Provider (res/xml/file_paths.xml)
```xml
<?xml version="1.0" encoding="utf-8"?>
<paths xmlns:android="http://schemas.android.com/apk/res/android">
    <external-files-path name="export" path="." />
</paths>
```

---

## 💻 Usage

### Starting the Service

1. **Enable Developer Options**
   - Settings > About Phone > Tap "Build Number" 7 times
   - Settings > Developer Options > Enable USB Debugging

2. **Choose Start Method**
   - **Wireless ADB**: Best for wireless operation
   - **USB ADB**: Requires USB connection
   - **Root**: Requires rooted device

3. **Start Service**
   - Open app > Home tab
   - Select method > Enter port (for wireless)
   - Tap "Start Service"

4. **Execute ADB Command** (for ADB methods)
   ```bash
   adb tcpip 5555
   adb shell sh /storage/emulated/0/Android/data/moe.shizuku.privileged/start.sh
   ```

### Creating Shortcuts

1. Navigate to **Shortcuts** tab
2. Tap **+ FAB button**
3. Fill in:
   - Name: "Disable Bloatware"
   - Icon: "🗑️"
   - Command: `pm disable-user --user 0 com.example.bloat`
   - Category: Package Manager
4. Tap **Create**
5. Execute by tapping ⚡ icon

### Creating Templates

1. Navigate to **Templates** tab
2. Tap **+ FAB button**
3. Fill in:
   - Name: "Uninstall App"
   - Command: `pm uninstall --user 0 {package}`
   - Description: "Uninstall app for current user"
4. Tap **Create**
5. Star it for quick access
6. Use in Executor

### Executing Commands

1. Navigate to **Executor** tab
2. Type command or use Quick Commands
3. Tap **Execute**
4. View output
5. Copy output if needed

### Browsing API Reference

1. Navigate to **API Reference** tab
2. Search for specific commands
3. Expand categories
4. Tap ▶️ to use in executor
5. Tap 📋 to copy command

---

## 📝 API Categories

### 1. Package Manager (12 commands)
- List packages (all/system/third-party/enabled/disabled)
- Install/Uninstall APK
- Enable/Disable apps
- Clear app data
- Grant/Revoke permissions

### 2. Activity Manager (6 commands)
- Start activities/services
- Broadcast intents
- Force stop apps
- Kill processes
- Open settings

### 3. App Ops (5 commands)
- Set/Get/Reset permissions
- Allow read logs
- Deny location

### 4. Settings (4 commands)
- Get/Put/Delete settings
- List all settings

### 5. DumpSys (6 commands)
- Battery/Display/Memory info
- CPU/Network stats
- WiFi details

### 6. Input & UI (6 commands)
- Tap screen
- Swipe gestures
- Send text
- Press buttons
- Get screen size

### 7. System Properties (5 commands)
- Device model/Android version
- SDK version/Manufacturer
- All properties

---

## 🔐 Permissions

### Runtime Permissions
The app requests these permissions at runtime:
- **WRITE_EXTERNAL_STORAGE** - For exporting data
- **Shizuku Permission** - For privilege elevation

### Requesting Permissions
```kotlin
val permissionLauncher = rememberLauncherForActivityResult(
    ActivityResultContracts.RequestMultiplePermissions()
) { /* Handle result */ }

permissionLauncher.launch(arrayOf(
    Manifest.permission.WRITE_EXTERNAL_STORAGE
))
```

---

## 🐛 Troubleshooting

### Service Won't Start
- ✅ Check ADB connection: `adb devices`
- ✅ Restart ADB: `adb kill-server && adb start-server`
- ✅ Re-enable wireless: `adb tcpip 5555`
- ✅ Verify Shizuku is installed and running

### Commands Fail
- ✅ Ensure service is running
- ✅ Check command syntax
- ✅ Replace placeholders
- ✅ View logs for errors

### Build Errors
```bash
# Clear cache
./gradlew clean
./gradlew --refresh-dependencies

# Invalidate caches
# Android Studio > File > Invalidate Caches / Restart
```

### Compose Version Mismatch
- Ensure `kotlinCompilerExtensionVersion` matches Kotlin version
- Use same Compose BOM for all dependencies

---

## 🚢 Building & Distribution

### Debug Build
```bash
./gradlew assembleDebug
# Output: app/build/outputs/apk/debug/app-debug.apk
```

### Release Build
```bash
./gradlew assembleRelease
# Output: app/build/outputs/apk/release/app-release-unsigned.apk
```

### Signed APK
1. Build > Generate Signed Bundle / APK
2. Create new keystore or use existing
3. Select release variant
4. Finish

### Distribution Options
- **GitHub Releases** - Host APK on GitHub
- **F-Droid** - Open source app store
- **Google Play Store** - Requires developer account
- **Direct APK** - Share via file/link

---

## 🧪 Testing

### Test Commands (Safe)
```bash
# Device info
getprop ro.product.model
getprop ro.build.version.release

# Battery
dumpsys battery

# Screen
wm size
wm density

# Packages
pm list packages | grep -i google
```

### Test Shortcuts
1. Create "Device Info" shortcut
2. Execute and verify output
3. Create "Battery" shortcut
4. Test multiple executions

### Test Templates
1. Create template with `{package}`
2. Load in executor
3. Replace placeholder
4. Execute and verify

---

## 📊 Performance

### Optimizations
- ✅ LazyColumn for scrolling lists
- ✅ State hoisting for recomposition
- ✅ remember for expensive operations
- ✅ Coroutines for async operations
- ✅ DataStore for efficient storage

### Memory Management
- Command output limited to prevent OOM
- Logs auto-trimmed after 1000 entries
- Images loaded efficiently
- Proper lifecycle handling

---

## 🔒 Security Considerations

### Important Notes
1. **ADB Debugging** is a security risk - disable when not needed
2. **Wireless ADB** - Only use on trusted networks
3. **Command Execution** - Review commands before execution
4. **Permissions** - Only grant necessary permissions
5. **Data Export** - Exported files contain sensitive data

### Best Practices
- ✅ Disable ADB when done
- ✅ Use USB ADB over Wireless when possible
- ✅ Review template commands
- ✅ Don't share APK with sensitive shortcuts
- ✅ Clear logs regularly

---

## 🤝 Contributing

### How to Contribute
1. Fork the repository
2. Create feature branch
3. Make changes
4. Test thoroughly
5. Submit pull request

### Code Style
- Follow Kotlin coding conventions
- Use meaningful variable names
- Add comments for complex logic
- Format with Android Studio
- Write tests where applicable

---

## 📄 License

This project is provided as-is for educational purposes.

**Disclaimer**: Modifying system apps and settings can potentially damage your device or void warranty. Use at your own risk.

---

## 🙏 Acknowledgments

- **Shizuku** - Inspiration and API
- **RikkaApps** - Rish tool
- **Android Open Source Project** - Shell command documentation
- **Jetpack Compose** - Modern UI toolkit
- **Material Design 3** - Design system

---

## 📞 Support

For issues or questions:
1. Check troubleshooting section
2. Review Android documentation
3. Test commands via ADB first
4. Check Android version compatibility
5. Open GitHub issue with details

---

## 🗺️ Roadmap

### v1.0.0 (Current) ✅
- [x] Service management
- [x] Custom shortcuts
- [x] Command templates
- [x] Command executor
- [x] API reference
- [x] Data persistence
- [x] Export functionality

### v1.1.0 (Planned)
- [ ] Import backup files
- [ ] Command history
- [ ] Favorites for API commands
- [ ] Scheduled commands
- [ ] Enhanced error messages
- [ ] Dark/Light theme toggle

### v1.2.0 (Future)
- [ ] Widgets support
- [ ] Tasker integration
- [ ] Multi-command execution
- [ ] Command queue
- [ ] Advanced logging
- [ ] Cloud sync (optional)

### v2.0.0 (Long-term)
- [ ] Plugin system
- [ ] Community templates
- [ ] Advanced automation
- [ ] Script editor
- [ ] Root mode enhancements
- [ ] Backup/Restore system apps

---

## 📸 Screenshots

*Add screenshots here after building the app*

---

## ⚡ Quick Start Commands

```bash
# Clone project
git clone <repository-url>
cd PrivilegeManagerPro

# Build
./gradlew assembleDebug

# Install
./gradlew installDebug

# Run
adb shell am start -n com.privilegemanager.pro/.MainActivity
```

---

## 📚 Additional Resources

- [Android Developers](https://developer.android.com/)
- [Jetpack Compose](https://developer.android.com/jetpack/compose)
- [Material Design 3](https://m3.material.io/)
- [Shizuku Documentation](https://shizuku.rikka.app/)
- [ADB Commands](https://developer.android.com/studio/command-line/adb)

---

**Version**: 1.0.0  
**Last Updated**: December 2024  
**Status**: Complete Native Android App ✅

---

## 🎉 Congratulations!

You now have a complete, native Android app with all features from the React prototype, plus native Android optimizations and Material Design 3 styling!
