# Memory Companion

> A Kotlin Multiplatform app that helps you remember important moments about the people in your life - with voice input and AI-powered insights.

[![Kotlin](https://img.shields.io/badge/Kotlin-2.0.21-blue.svg)](https://kotlinlang.org)
[![Compose Multiplatform](https://img.shields.io/badge/Compose%20Multiplatform-1.7.0-brightgreen)](https://www.jetbrains.com/lp/compose-multiplatform/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

<div align="center">
  <img src="screenshots/01-person-list.png" alt="Memory Companion Banner" width="700"/>
</div>

---

## The Problem

We all struggle to remember important details about the people in our lives:
- When did I last talk to Sarah about her project?
- What was that deadline John mentioned?
- What's causing stress for my team members?

Traditional note-taking apps require:
- Tedious manual typing
- Manual searching through scattered notes
- Organizing and categorizing everything yourself
- Remembering to write things down in the first place

**Information gets lost. Context disappears. Memories fade.**

---

## The Solution

Memory Companion makes capturing and querying personal memories **effortless and intelligent**.

### Voice Input - Speak, Don't Type

<div align="center">
  <img src="screenshots/02-voice-input.png" alt="Voice Input" width="600"/>
</div>

Press and hold the microphone button. Speak naturally:

> *"I had lunch with Sarah today at the Italian restaurant. She told me about her new project deadline next Friday and she's feeling stressed about the budget."*

The app transcribes everything automatically using platform-native speech recognition. **No typing required.**

---

### AI Analysis - Automatic Context Extraction

<div align="center">
  <img src="screenshots/03-ai-review.png" alt="AI Review" width="600"/>
</div>

Powered by **Google Gemini AI**, the app automatically extracts:

- **Topic:** "Work Discussion"
- **Emotion:** "Stressed"
- **Time Reference:** "Next Friday"
- **Action Items:** "Follow up on budget discussion"
- **Key Details:** "Italian restaurant, project deadline, budget concerns"
- **Summary:** Concise AI-generated summary

**All extracted in seconds, ready for your review.**

---

### Ethical Design - You Stay in Control

<div align="center">
  <img src="screenshots/03-ai-review.png" alt="Consent Screen" width="600"/>
</div>

**Nothing is saved without your explicit approval.**

- Review all AI-extracted information
- Edit any field before saving
- Discard if the analysis is wrong
- **Privacy and consent first, always**

This isn't just a feature - it's a core design principle. Your memories, your control.

---

### Smart Queries - Ask in Natural Language

<div align="center">
  <img src="screenshots/05-chat-query.png" alt="Chat Query" width="600"/>
</div>

No need to search manually. Just ask:

- *"When is Sarah's project deadline?"*
- *"What is John stressed about?"*
- *"Who did I meet last week?"*
- *"What did Sarah tell me about the budget?"*

The AI searches your memories and provides **answers with source citations**. Tap to expand and see exactly which memories were used.

---

### Cross-Platform - One Codebase, Two Platforms

<div align="center">
  <img src="screenshots/06-desktop-version.png" alt="Desktop Version" width="700"/>
</div>

Built with **Kotlin Multiplatform** - not a web wrapper, not a hybrid app. **Real native performance** on both platforms.

<div align="center">

| Feature | Android | Windows Desktop |
|:--------|:-------:|:---------------:|
| Person Management | ✅ | ✅ |
| Memory Storage | ✅ | ✅ |
| AI Analysis (Gemini) | ✅ | ✅ |
| Natural Language Chat | ✅ | ✅ |
| Voice Input | ✅ | ⚠️ Not yet |
| Offline-First Database | ✅ | ✅ |

</div>

**90%+ code sharing.** Single team, single codebase, multiple platforms.

---

## Tech Stack

### Core Technologies

<table>
<tr>
<td width="50%">

**Language & Framework**
- Kotlin 2.0.21
- Kotlin Multiplatform (KMP)
- Jetpack Compose Multiplatform 1.7.0

</td>
<td width="50%">

**Architecture**
- MVVM Pattern
- Clean Architecture
- Unidirectional Data Flow
- Reactive Programming (Flow)

</td>
</tr>
</table>

### Key Libraries

| Library | Purpose | Version |
|---------|---------|:-------:|
| **Room** | Local SQLite database with KMP support | 2.7.0-alpha01 |
| **Ktor** | HTTP client for Gemini API | Latest |
| **Koin** | Dependency injection | Latest |
| **Kotlinx Serialization** | JSON parsing | Latest |
| **Kotlinx Coroutines** | Asynchronous programming | Latest |
| **Material 3** | Modern UI design system | Latest |

### AI & Platform-Specific

- **Google Gemini AI** - `gemini-2.5-flash` model for natural language processing
- **Android Speech Recognition** - Native `android.speech.SpeechRecognizer`
- **Platform-Specific Implementations** - KMP `expect`/`actual` pattern

---

## Architecture Overview

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

### Platform-Specific Code (KMP expect/actual)

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

**This pattern is used for:**
- Speech recognition
- Database builders
- API key storage (BuildConfig vs System properties)

---

## Installation & Setup

### Prerequisites

- **JDK 17 or higher** ([Eclipse Temurin](https://adoptium.net/) recommended)
- **Android Studio Ladybug (2024.2.1)** or later
- **Gradle 8.5+** (included via wrapper)
- **Google Gemini API Key** (free tier available)

### Step 1: Clone the Repository

```bash
git clone https://github.com/harshk160/Memory-Companion-KotlinConf-2026.git
cd Memory-Companion-KotlinConf-2026
```

### Step 2: Get a Gemini API Key

1. Visit [Google AI Studio](https://aistudio.google.com/)
2. Sign in with your Google account
3. Click **"Get API Key"**
4. Create a new API key for your project
5. Copy the key (starts with `AIza...`)

### Step 3: Configure the API Key

Create a `local.properties` file in the project root directory:

```properties
# local.properties
GEMINI_API_KEY=AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
```

> **⚠️ Important:** This file is already in `.gitignore`. Never commit your API key to version control!

### Step 4: Build & Run

<details>
<summary><b>Android</b></summary>

**Using Android Studio:**
1. Open the project in Android Studio
2. Wait for Gradle sync to complete
3. Select `composeApp` run configuration
4. Click **Run** (or press Shift+F10)

**Using Command Line:**
```bash
# Build APK
./gradlew :composeApp:assembleDebug

# Install to connected device
adb install composeApp/build/outputs/apk/debug/composeApp-debug.apk
```

</details>

<details>
<summary><b>Windows Desktop</b></summary>

> **Note:** Requires a full JDK (not Android Studio's embedded JDK).

**Using Command Line:**
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

**Troubleshooting:**
If build fails with "jpackage.exe missing":
1. Download [Eclipse Temurin JDK 17](https://adoptium.net/)
2. In Android Studio: File → Settings → Build Tools → Gradle
3. Set Gradle JDK to your installed Temurin JDK
4. Re-run the build

</details>

---

## User Guide

### First Launch

1. Launch the app
2. **(Android only)** Grant microphone permission when prompted
3. You'll see an empty person list - let's add your first person!

### Adding Your First Person

1. Tap the **+** button at the bottom
2. Enter a name (e.g., "Sarah")
3. Tap **Add**

### Recording a Memory

<details>
<summary><b>Using Voice Input (Recommended)</b></summary>

1. Tap the **Add Memory** button
2. Select a person from the dropdown
3. **Press and hold** the microphone button
4. **Speak clearly:** *"I had coffee with Sarah and she mentioned her vacation plans for March"*
5. Release the button
6. The transcribed text appears instantly

</details>

<details>
<summary><b>Using Text Input</b></summary>

1. Tap the **Add Memory** button
2. Select a person from the dropdown
3. Type in the large text field
4. The text will be analyzed when you proceed

</details>

### Reviewing AI Analysis

After adding a memory, you'll see the AI review screen:

1. **Review** the AI-extracted information (topic, emotion, deadlines, etc.)
2. **Edit** any field if the AI got something wrong
3. Choose one of three options:
   - **Confirm & Save** - Saves to database
   - **Edit** - Toggle edit mode for corrections
   - **Discard** - Go back without saving

### Querying Your Memories

1. Tap the **Chat** button
2. Ask a question: *"When did I last talk to Sarah?"*
3. Wait for the AI to search and respond
4. Tap **"source memories"** to see which memories were used

### Viewing Person Details

1. Tap any person card on the main screen
2. See all memories associated with that person
3. View memory count, timestamps, and content

---

## Testing & Verification

### Tested Configurations

| Platform | Device/OS | Status |
|----------|-----------|:------:|
| Android | Xiaomi Physical Device (Android 12) | ✅ Fully Working |
| Android | Pixel 6 Emulator (API 34) | ✅ Working* |
| Windows | Windows 11 Desktop | ✅ Working** |

**\*Voice may not work on emulator**  
**\*\*Except voice input (graceful error shown)**

### Known Limitations

- Voice input requires Google Play Services on Android
- Desktop voice input not yet implemented (shows user-friendly error)
- Some Android emulators don't support speech recognition
- Internet connection required for AI analysis (memories stored offline)

### Performance Metrics

- ✅ Tested with 50+ memories - smooth performance
- ✅ Database operations under 100ms
- ✅ AI analysis typically completes in 2-5 seconds
- ✅ Memory usage stable under 150MB

---

## Project Structure

<details>
<summary><b>Click to expand full project structure</b></summary>

```
memory-companion/
├── composeApp/
│   ├── src/
│   │   ├── androidMain/              # Android-specific (5%)
│   │   │   └── kotlin/
│   │   │       └── com/harsh/myapplication/
│   │   │           ├── MainActivity.kt
│   │   │           ├── MyApplication.kt
│   │   │           └── data/
│   │   │               ├── local/DatabaseBuilder.android.kt
│   │   │               └── speech/SpeechRecognizer.android.kt
│   │   │
│   │   ├── jvmMain/                  # Desktop-specific (5%)
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

</details>

### Code Statistics

- **Total Lines:** ~3,500 lines of Kotlin code
- **Code Sharing:** 90%+ between platforms
- **Screens:** 6 main screens
- **Components:** 4 reusable components
- **ViewModels:** 5 ViewModels
- **Repositories:** 2 repositories

---

## Privacy & Security

### Data Storage
- ✅ All data stored **locally** in SQLite database
- ✅ No cloud sync (your data never leaves your device)
- ✅ No user accounts or authentication required
- ⚠️ Gemini API calls send memory text for analysis

### API Key Security
- ✅ API key stored in `local.properties` (gitignored)
- ✅ Injected at **build time** via Gradle
- ✅ Never hardcoded in source code
- ✅ Platform-specific secure access

### User Consent
- ✅ AI analysis shown to user **before** saving
- ✅ User can **edit or reject** any AI-generated content
- ✅ Explicit **"Confirm & Save"** button required
- ✅ No automatic background processing

---

## Troubleshooting

<details>
<summary><b>"Unresolved reference: GEMINI_API_KEY"</b></summary>

**Solution:**
1. Create `local.properties` file in project root
2. Add: `GEMINI_API_KEY=your_actual_key_here`
3. Sync Gradle in Android Studio

</details>

<details>
<summary><b>Voice input shows "Permission denied"</b></summary>

**Solution:**
1. Open Android Settings
2. Go to: Settings → Apps → Memory Companion → Permissions
3. Enable **Microphone** permission

</details>

<details>
<summary><b>Desktop app won't build (jpackage missing)</b></summary>

**Solution:**
1. Install full [Eclipse Temurin JDK 17](https://adoptium.net/)
2. In Android Studio: File → Settings → Build Tools → Gradle
3. Set Gradle JDK to your Temurin installation
4. Don't use Android Studio's embedded JDK

</details>

<details>
<summary><b>Emulator voice input not working</b></summary>

**This is expected behavior:**
- Most Android emulators don't support speech recognition
- Use a real physical device for voice input testing
- You can still type memories manually on emulator

</details>

<details>
<summary><b>"Network error" when analyzing memory</b></summary>

**Check these:**
- ✅ Internet connection is active
- ✅ API key is correct in `local.properties`
- ✅ Gemini API quota not exceeded (free tier has limits)

</details>

---

## Future Roadmap

Potential enhancements for v2.0:

- [ ] **iOS Support** - Extend to Apple ecosystem
- [ ] **Cloud Sync** - Encrypted backup and multi-device sync
- [ ] **Desktop Voice Input** - Using third-party library
- [ ] **Photo Attachments** - Add images to memories
- [ ] **Timeline View** - Visual calendar of memories
- [ ] **Smart Reminders** - "You haven't checked in with Sarah in 2 weeks"
- [ ] **Analytics Dashboard** - Insights about your social connections
- [ ] **Multi-language Support** - Internationalization
- [ ] **Export Features** - PDF/CSV export for backup
- [ ] **End-to-End Encryption** - For cloud sync

---

## Contributing

This project was built for the **Kotlin Multiplatform Contest**, but contributions are welcome!

### How to Contribute

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes and commit: `git commit -m 'Add some amazing feature'`
4. Push to your fork: `git push origin feature/amazing-feature`
5. Open a Pull Request

### Development Guidelines

- Follow Kotlin coding conventions
- Write meaningful commit messages
- Add tests for new features (when applicable)
- Update documentation for user-facing changes
- Ensure both Android and Desktop builds pass

---

## License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

---

## Author

**Harsh Kumar**

<div align="center">

[![GitHub](https://img.shields.io/badge/GitHub-harshk160-181717?style=for-the-badge&logo=github)](https://github.com/harshk160)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Harsh%20Kumar-0077B5?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/harsh-kumar-30a45928b/)
[![Email](https://img.shields.io/badge/Email-harshkr1608%40gmail.com-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:harshkr1608@gmail.com)

</div>

---

## Acknowledgments

- **Google Gemini AI** - For powerful natural language processing capabilities
- **JetBrains** - For Kotlin Multiplatform and Compose Multiplatform
- **Android Community** - For excellent KMP resources and documentation
- **Kotlin Multiplatform Contest** - For the motivation to build this project
- **Open Source Community** - For the libraries that made this possible

---

## Contest Submission

<div align="center">

| Item | Details |
|:-----|:--------|
| **Contest** | Kotlin Multiplatform Contest |
| **Category** | Kotlin Multiplatform |
| **Submission Date** | January 12, 2026 |
| **Repository** | [github.com/harshk160/Memory-Companion-KotlinConf-2026](https://github.com/harshk160/Memory-Companion-KotlinConf-2026) |

</div>

---

## Stats & Metrics

<div align="center">

| Metric | Value |
|:-------|:------|
| **Development Time** | 6 weeks (Dec 2025 - Jan 2026) |
| **Lines of Code** | ~3,500 |
| **Code Sharing** | 90%+ between platforms |
| **Dependencies** | 10 major libraries |
| **Build Time** | 3 min (Android) / 1 min (Desktop) |
| **App Size** | 27MB (APK) / 101MB (MSI) |

</div>

---

<div align="center">

### Built with ❤️ using Kotlin Multiplatform

[Report Bug](https://github.com/harshk160/Memory-Companion-KotlinConf-2026/issues) · [Request Feature](https://github.com/harshk160/Memory-Companion-KotlinConf-2026/issues)

---

**⭐ Star this repo if you found it useful!**

*Last Updated: January 12, 2026*

</div>