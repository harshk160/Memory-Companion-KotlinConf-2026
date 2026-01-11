# 🧠 Memory Companion

> A Kotlin Multiplatform app that helps you remember important moments about the people in your life - with voice input and AI-powered insights.

[![Kotlin](https://img.shields.io/badge/Kotlin-2.0.21-blue.svg)](https://kotlinlang.org)
[![Compose Multiplatform](https://img.shields.io/badge/Compose%20Multiplatform-1.7.0-brightgreen)](https://www.jetbrains.com/lp/compose-multiplatform/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

![Memory Companion Banner](screenshots/01-person-list.png)

## 🎥 Demo Video

**Watch the full demo:** [YouTube Demo Video - Coming Soon]

> *A 3-minute walkthrough showing voice input, AI analysis, natural language queries, and cross-platform capabilities.*

---

## 💡 The Problem

We all struggle to remember important details about the people in our lives:
- 🤔 "When did I last talk to Sarah about her project?"
- 📅 "What was that deadline John mentioned?"
- 💼 "What's causing stress for my team members?"

Traditional note-taking apps require:
- ⌨️ Tedious manual typing
- 🔍 Manual searching through scattered notes
- 🗂️ Organizing and categorizing everything yourself
- 🧠 Remembering to write things down in the first place

**Information gets lost. Context disappears. Memories fade.**

---

## ✨ The Solution

Memory Companion makes capturing and querying personal memories **effortless and intelligent**.

### 🎤 **Voice Input** - Speak, Don't Type

![Voice Input](screenshots/02-voice-input.png)

Press and hold the microphone button. Speak naturally:

> "I had lunch with Sarah today at the Italian restaurant. She told me about her new project deadline next Friday and she's feeling stressed about the budget."

The app transcribes everything automatically using platform-native speech recognition. **No typing required.**

---

### 🤖 **AI Analysis** - Automatic Context Extraction

![AI Review](screenshots/03-ai-review.png)

Powered by **Google Gemini AI**, the app automatically extracts:

- **📝 Topic:** "Work Discussion"
- **😰 Emotion:** "Stressed"
- **📅 Time Reference:** "Next Friday"
- **✅ Action Items:** "Follow up on budget discussion"
- **🔑 Key Details:** "Italian restaurant, project deadline, budget concerns"
- **📄 Summary:** Concise AI-generated summary

**All extracted in seconds, ready for your review.**

---

### ✅ **Ethical Design** - You Stay in Control

![Consent Screen](screenshots/03-ai-review.png)

**Nothing is saved without your explicit approval.**

- Review all AI-extracted information
- Edit any field before saving
- Discard if the analysis is wrong
- **Privacy and consent first, always**

This isn't just a feature - it's a core design principle. Your memories, your control.

---

### 💬 **Smart Queries** - Ask in Natural Language

![Chat Query](screenshots/05-chat-query.png)

No need to search manually. Just ask:

- *"When is Sarah's project deadline?"*
- *"What is John stressed about?"*
- *"Who did I meet last week?"*
- *"What did Sarah tell me about the budget?"*

The AI searches your memories and provides **answers with source citations**. Tap to expand and see exactly which memories were used.

---

### 📱💻 **Cross-Platform** - One Codebase, Two Platforms

![Desktop Version](screenshots/06-desktop-version.png)

Built with **Kotlin Multiplatform** - not a web wrapper, not a hybrid app. **Real native performance** on both platforms.

| Feature | Android | Windows Desktop |
|---------|---------|-----------------|
| Person Management | ✅ | ✅ |
| Memory Storage | ✅ | ✅ |
| AI Analysis (Gemini) | ✅ | ✅ |
| Natural Language Chat | ✅ | ✅ |
| Voice Input | ✅ | ⚠️ Not yet (graceful error) |
| Offline-First Database | ✅ | ✅ |

**90%+ code sharing.** Single team, single codebase, multiple platforms.

---

## 🛠️ Tech Stack

### **Core Technologies**

- **Kotlin 2.0.21** - Modern, type-safe language
- **Kotlin Multiplatform (KMP)** - Shared business logic across platforms
- **Jetpack Compose Multiplatform 1.7.0** - Declarative UI framework

### **Architecture**

- **MVVM Pattern** - Clear separation of concerns
- **Clean Architecture** - UI → ViewModel → Repository → Data Source
- **Unidirectional Data Flow** - Predictable state management
- **Reactive Programming** - Kotlinx Flow for real-time updates

### **Key Libraries**

| Library | Purpose | Version |
|---------|---------|---------|
| **Room** | Local SQLite database with KMP support | 2.7.0-alpha01 |
| **Ktor** | HTTP client for Gemini API | Latest |
| **Koin** | Dependency injection | Latest |
| **Kotlinx Serialization** | JSON parsing | Latest |
| **Kotlinx Coroutines** | Asynchronous programming | Latest |
| **Material 3** | Modern UI design system | Latest |

### **AI & Platform-Specific**

- **Google Gemini AI** - `gemini-2.5-flash` model for natural language processing
- **Android Speech Recognition** - Native `android.speech.SpeechRecognizer`
- **Platform-Specific Implementations** - KMP `expect`/`actual` pattern

---

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────────────────────┐
│                    UI Layer (Compose)                   │
│   PersonListScreen │ AddMemoryScreen │ ChatScreen       │
│   PersonDetailScreen │ MemoryReviewScreen               │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│                  ViewModel Layer                        │
│        State Management │ Business Logic                │
│   PersonListVM │ AddMemoryVM │ ChatVM │ ReviewVM        │
└────────────────────────┬────────────────────────────────┘
                         │
┌────────────────────────▼────────────────────────────────┐
│                 Repository Layer                        │
│        PersonRepository │ MemoryRepository              │
│         (Error Handling & Data Mapping)                 │
└──────────────┬──────────────────────┬───────────────────┘
               │                      │
┌──────────────▼──────────┐  ┌───────▼──────────────────┐
│     Room Database       │  │   GeminiService (Ktor)   │
│   PersonDao │ MemoryDao │  │  AI Analysis & Queries   │
│   (Local SQLite)        │  │  (Remote API)            │
└─────────────────────────┘  └──────────────────────────┘
```

### **Platform-Specific Code (KMP expect/actual)**

```kotlin
// Common Interface (expect)
expect class SpeechRecognizer {
    fun startListening(onResult: (SpeechRecognizerState) -> Unit)
    fun stopListening()
}

// Android Implementation (actual)
actual class SpeechRecognizer(context: Context) {
    // Uses android.speech.SpeechRecognizer
}

// Desktop Implementation (actual)
actual class SpeechRecognizer {
    // Graceful fallback - shows "Not supported" message
}
```

This pattern is used for:
- 🎤 Speech recognition
- 💾 Database builders
- 🔐 API key storage (BuildConfig vs System properties)

---

## 📦 Installation & Setup

### **Prerequisites**

- **JDK 17 or higher** ([Eclipse Temurin](https://adoptium.net/) recommended)
- **Android Studio Ladybug (2024.2.1)** or later
- **Gradle 8.5+** (included via wrapper)
- **Google Gemini API Key** (free tier available)

### **Step 1: Clone the Repository**

```bash
git clone https://github.com/harshk160/Memory-Companion-KotlinConf-2026.git
cd Memory-Companion-KotlinConf-2026
```

### **Step 2: Get a Gemini API Key**

1. Visit [Google AI Studio](https://aistudio.google.com/)
2. Sign in with your Google account
3. Click **"Get API Key"**
4. Create a new API key for your project
5. Copy the key (starts with `AIza...`)

### **Step 3: Configure the API Key**

Create a `local.properties` file in the project root directory:

```properties
# local.properties
GEMINI_API_KEY=AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

⚠️ **Important:** This file is already in `.gitignore`. Never commit your API key to version control!

### **Step 4: Build & Run**

#### **Option A: Android**

Using Android Studio:
1. Open the project in Android Studio
2. Wait for Gradle sync to complete
3. Select `composeApp` run configuration
4. Click **Run ▶️** (or press Shift+F10)

Using Command Line:
```bash
# Build APK
./gradlew :composeApp:assembleDebug

# Install to connected device
adb install composeApp/build/outputs/apk/debug/composeApp-debug.apk
```

#### **Option B: Windows Desktop**

**Important:** Requires a **full JDK** (not Android Studio's embedded JDK).

Using Command Line:
```bash
# Run directly with API key as argument
./gradlew :composeApp:run -PgeminiApiKey=YOUR_API_KEY_HERE

# Or build an installer
./gradlew :composeApp:packageDistributionForCurrentOS
```

The installer will be generated at:
```
composeApp/build/compose/binaries/main/msi/Memory-Companion-1.0.0.msi
```

**Troubleshooting Desktop Build:**
If `packageDistributionForCurrentOS` fails with "jpackage.exe missing":
1. Download [Eclipse Temurin JDK 17](https://adoptium.net/)
2. In Android Studio: File → Settings → Build Tools → Gradle
3. Set Gradle JDK to your installed Temurin JDK
4. Re-run the build

---

## 🎮 User Guide

### **First Launch**

1. Launch the app
2. **(Android only)** Grant microphone permission when prompted
3. You'll see an empty person list

### **Adding Your First Person**

1. Tap the **+** (plus) button at the bottom
2. Enter a name (e.g., "Sarah")
3. Tap **Add**

### **Recording a Memory (Voice Input)** 🎤

1. Tap the **🔍** button (Add Memory)
2. Select a person from the dropdown
3. **Press and hold** the 🎤 microphone button
4. **Speak clearly:** "I had coffee with Sarah and she mentioned her vacation plans for March"
5. Release the button
6. The transcribed text appears instantly!

### **Recording a Memory (Text Input)** ⌨️

1. Tap the **🔍** button (Add Memory)
2. Select a person from the dropdown
3. Type in the large text field
4. Text will be analyzed when you proceed

### **Reviewing AI Analysis** ✅

After adding a memory:
1. Review the AI-extracted information (topic, emotion, etc.)
2. **Edit any field** if the AI got something wrong
3. Choose:
   - **Confirm & Save** - Saves to database
   - **Edit** - Toggle edit mode for corrections
   - **Discard** - Go back without saving

### **Querying Your Memories** 💬

1. Tap the **💬** button (Chat)
2. Ask a question: "When did I last talk to Sarah?"
3. Wait for the AI to search and respond
4. Tap **"📚 X source memories"** to see which memories were used

### **Viewing Person Details**

1. Tap any person card on the main screen
2. See all memories associated with that person
3. View memory count, timestamps, and content

---

## 🧪 Testing & Verification

### **Tested Configurations**

| Platform | Device/OS | Status |
|----------|-----------|--------|
| Android | Xiaomi Physical Device (Android 13) | ✅ Fully Working |
| Android | Pixel 6 Emulator (API 34) | ✅ Working (voice may not work on emulator) |
| Windows | Windows 11 Desktop | ✅ Working (except voice input) |

### **Known Limitations**

- 🎤 Voice input requires **Google Play Services** on Android
- 🖥️ Desktop voice input not yet implemented (shows user-friendly error message)
- 📱 Some Android emulators don't support speech recognition (use real device)
- 🌐 Requires internet connection for AI analysis (memories stored offline)

### **Performance**

- ⚡ Tested with 50+ memories - smooth performance
- 💾 Database operations under 100ms
- 🤖 AI analysis typically completes in 2-5 seconds
- 📊 Memory usage stable under 150MB

---

## 🗂️ Project Structure

```
memory-companion/
├── composeApp/
│   ├── src/
│   │   ├── androidMain/              # Android-specific
│   │   │   └── kotlin/
│   │   │       └── com/harsh/myapplication/
│   │   │           ├── MainActivity.kt
│   │   │           ├── MyApplication.kt
│   │   │           └── data/
│   │   │               ├── local/DatabaseBuilder.android.kt
│   │   │               └── speech/SpeechRecognizer.android.kt
│   │   │
│   │   ├── jvmMain/                  # Desktop-specific
│   │   │   └── kotlin/
│   │   │       └── com/harsh/myapplication/
│   │   │           ├── main.kt
│   │   │           └── data/
│   │   │               ├── local/DatabaseBuilder.jvm.kt
│   │   │               └── speech/SpeechRecognizer.jvm.kt
│   │   │
│   │   └── commonMain/               # Shared code (90%+)
│   │       └── kotlin/
│   │           └── com/harsh/myapplication/
│   │               ├── App.kt
│   │               ├── data/
│   │               │   ├── local/       # Database
│   │               │   ├── model/       # Data models
│   │               │   ├── remote/      # Gemini API
│   │               │   ├── repository/  # Data layer
│   │               │   └── speech/      # Voice (expect)
│   │               ├── di/              # Koin DI
│   │               └── ui/
│   │                   ├── components/  # Reusable UI
│   │                   ├── screens/     # Main screens
│   │                   └── viewmodel/   # Business logic
│   └── build.gradle.kts
├── gradle/
│   └── libs.versions.toml            # Version catalog
├── local.properties                  # API keys (gitignored)
├── README.md
└── LICENSE
```

**Code Statistics:**
- ~3,500 lines of Kotlin code
- 90%+ code shared between platforms
- 6 main screens
- 4 reusable components
- 5 ViewModels
- 2 repositories
- Clean architecture with clear separation

---

## 🔒 Privacy & Security

### **Data Storage**
- ✅ All data stored **locally** in SQLite database
- ✅ No cloud sync (your data never leaves your device)
- ✅ No user accounts or authentication required
- ⚠️ Gemini API calls send memory text for analysis (see API key security)

### **API Key Security**
- ✅ API key stored in `local.properties` (gitignored)
- ✅ Injected at **build time** via Gradle
- ✅ Never hardcoded in source code
- ✅ Platform-specific access:
  - Android: `BuildConfig.GEMINI_API_KEY`
  - Desktop: `System.getProperty("gemini.api.key")`

### **User Consent**
- ✅ AI analysis shown to user **before** saving
- ✅ User can **edit or reject** any AI-generated content
- ✅ Explicit **"Confirm & Save"** button required
- ✅ No automatic background processing
- ✅ Transparent about what data is stored

---

## 🐛 Troubleshooting

### **"Unresolved reference: GEMINI_API_KEY"**
- ✅ Create `local.properties` file in project root
- ✅ Add: `GEMINI_API_KEY=your_actual_key_here`
- ✅ Sync Gradle

### **Voice input shows "Permission denied"**
- ✅ Grant microphone permission in Android settings
- ✅ Check: Settings → Apps → Memory Companion → Permissions → Microphone

### **Desktop app won't build (jpackage missing)**
- ✅ Install full JDK 17 (Eclipse Temurin)
- ✅ Set Gradle JDK in Android Studio settings
- ✅ Don't use Android Studio's embedded JDK

### **Emulator voice input not working**
- ✅ This is expected - use a real Android device
- ✅ Most emulators don't support speech recognition
- ✅ You can still type memories manually

### **"Network error" when analyzing memory**
- ✅ Check internet connection
- ✅ Verify API key is correct
- ✅ Check Gemini API quota (free tier limits)

---

## 🚧 Future Roadmap

Potential enhancements for v2.0:

- [ ] 📱 **iOS Support** - Extend to Apple ecosystem
- [ ] ☁️ **Cloud Sync** - Encrypted backup and multi-device sync
- [ ] 🎙️ **Desktop Voice Input** - Using third-party library
- [ ] 📸 **Photo Attachments** - Add images to memories
- [ ] 📅 **Timeline View** - Visual calendar of memories
- [ ] 🔔 **Smart Reminders** - "You haven't checked in with Sarah in 2 weeks"
- [ ] 📊 **Analytics Dashboard** - Insights about your social connections
- [ ] 🌍 **Multi-language Support** - Internationalization
- [ ] 📤 **Export Features** - PDF/CSV export for backup
- [ ] 🔐 **End-to-End Encryption** - For cloud sync

**Want to contribute?** Open an issue or PR!

---

## 🤝 Contributing

This project was built for the **KotlinConf 2026 Contest**, but contributions are welcome!

### **How to Contribute**

1. Fork the repository
2. Create a feature branch:
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. Make your changes and commit:
   ```bash
   git commit -m 'Add some amazing feature'
   ```
4. Push to your fork:
   ```bash
   git push origin feature/amazing-feature
   ```
5. Open a Pull Request

### **Development Guidelines**

- Follow Kotlin coding conventions
- Write meaningful commit messages
- Add tests for new features (when applicable)
- Update documentation for user-facing changes
- Ensure both Android and Desktop builds pass

---

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

**TL;DR:** You can use, modify, and distribute this code freely, even commercially. Just include the original copyright notice.

---

## 👤 Author

**Harsh Kumar**

- 🐙 GitHub: [@harshk160](https://github.com/harshk160)
- 📧 Email: harsh.k160@example.com *(update with your actual email)*
- 💼 LinkedIn: [Harsh Kumar](https://linkedin.com/in/harsh-kumar) *(update with your profile)*
- 🌐 Portfolio: [harshkumar.dev](https://harshkumar.dev) *(optional)*

---

## 🙏 Acknowledgments

- **Google Gemini AI** - For powerful natural language processing capabilities
- **JetBrains** - For Kotlin Multiplatform and Compose Multiplatform
- **Android Community** - For excellent KMP resources and documentation
- **KotlinConf 2026 Contest** - For the motivation to build this project!
- **Open Source Community** - For the libraries that made this possible

---

## 🏆 Contest Submission

- **Contest:** KotlinConf 2026 Global Contest
- **Category:** Kotlin Multiplatform
- **Submission Date:** January 2026
- **Repository:** [github.com/harshk160/Memory-Companion-KotlinConf-2026](https://github.com/harshk160/Memory-Companion-KotlinConf-2026)
- **Demo Video:** [YouTube Link - Coming Soon]

---

## 📊 Stats & Metrics

- **Development Time:** 6 weeks (Dec 2025 - Jan 2026)
- **Lines of Code:** ~3,500
- **Code Sharing:** 90%+ between platforms
- **Dependencies:** 10 major libraries
- **Build Time:** ~3 minutes (Android), ~1 minute (Desktop)
- **App Size:** ~25MB (Android APK), ~80MB (Windows installer)

---

<div align="center">

**Built with ❤️ using Kotlin Multiplatform**

⭐ Star this repo if you found it useful!

[Report Bug](https://github.com/harshk160/Memory-Companion-KotlinConf-2026/issues) · [Request Feature](https://github.com/harshk160/Memory-Companion-KotlinConf-2026/issues) · [Documentation](https://github.com/harshk160/Memory-Companion-KotlinConf-2026/wiki)

</div>

---

## 🔗 Quick Links

- 📺 [Watch Demo Video](#-demo-video)
- 📥 [Installation Guide](#-installation--setup)
- 📖 [User Guide](#-user-guide)
- 🏗️ [Architecture](#️-architecture-overview)
- 🐛 [Troubleshooting](#-troubleshooting)
- 🤝 [Contributing](#-contributing)

---

*Last Updated: January 11, 2026*