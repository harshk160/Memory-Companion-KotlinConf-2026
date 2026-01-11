# Memory Companion

**Memory Companion** is a cross-platform application built with **Kotlin Multiplatform (KMP)** that serves as an intelligent personal assistant for managing your memories and relationships. It allows users to store details about people and shared experiences, and then uses **Google Gemini AI** to enable natural language queries about that data.

*Built for the KotlinConf 2026 Student Coding Competition.*

## 🚀 Features

* **🧠 AI-Powered Recall:** Chat with your companion to ask questions like *"What did I gift John last Christmas?"* or *"When did I last meet Sarah?"* using Google Gemini.
* **📱 Cross-Platform:** Runs natively on **Android** and **Desktop (JVM)** with a 100% shared UI codebase.
* **🎙️ Voice Input:** Integrated Speech-to-Text allows for hands-free memory logging and querying.
* **💾 Local-First Persistence:** Uses **Room Database** (SQLite) to store all personal data securely on the device.
* **🎨 Modern UI:** Built entirely with **Compose Multiplatform** and Material 3 design.

## 🛠️ Tech Stack

This project demonstrates the power of the Kotlin ecosystem by leveraging modern Multiplatform libraries:

* **Language:** Kotlin 2.0
* **UI:** Compose Multiplatform (Material 3)
* **Navigation:** Voyager
* **Dependency Injection:** Koin
* **Database:** Room Multiplatform (SQLite)
* **Networking & AI:** Ktor Client + Google Gemini API
* **Asynchronous:** Kotlin Coroutines & Flow
* **Serialization:** Kotlinx Serialization

## 📸 Screenshots

| Android Home | Person Detail | AI Chat Query | Desktop App |
|:---:|:---:|:---:|:---:|
| | | | |

*(Judges: Please see the `screenshots` folder for high-res images if not loading)*

## 🏃‍♂️ How to Run

### Prerequisites
* JDK 17 or higher
* Android Studio Ladybug (or newer) / IntelliJ IDEA

### Step 1: Clone and Setup
Clone the repository:
```bash
git clone [https://github.com/YOUR_USERNAME/Memory-Companion.git](https://github.com/YOUR_USERNAME/Memory-Companion.git)
cd Memory-Companion