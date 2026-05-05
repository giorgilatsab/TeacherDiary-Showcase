<div align="center">

# 📚 Teacher Diary

### *The all-in-one digital diary for private tutors and educators — built for the modern teacher.*

Track students, schedule lessons, manage payments, and stay connected with parents — all in one polished, multilingual app.

<br/>

![Platform](https://img.shields.io/badge/Platform-Android-3DDC84?style=for-the-badge&logo=android&logoColor=white)
![Language](https://img.shields.io/badge/Language-Kotlin-7F52FF?style=for-the-badge&logo=kotlin&logoColor=white)
![Min SDK](https://img.shields.io/badge/Min%20SDK-26-blue?style=for-the-badge)
![Target SDK](https://img.shields.io/badge/Target%20SDK-35-blue?style=for-the-badge)
![Material 3](https://img.shields.io/badge/Material-3-757575?style=for-the-badge&logo=materialdesign&logoColor=white)
![Languages](https://img.shields.io/badge/Languages-7-orange?style=for-the-badge)

<br/>

[**📱 Get it on Google Play**](#) · [**🎬 Watch Demo**](#) · [**📖 Documentation**](#)

</div>

---

## 🎯 What is Teacher Diary?

**Teacher Diary** is a modern Android application crafted for private tutors, music teachers, language instructors, and after-school educators. It replaces the traditional pen-and-paper notebook with a smart digital workflow that helps teachers focus on what matters most — teaching.

Whether you teach one student or manage twenty groups, Teacher Diary scales with you: track every lesson, monitor payments, communicate with parents via WhatsApp or SMS, and visualize your earnings — all in your native language.

> **Built for the global teacher.** Available in 7 languages with full international phone number support, the app works seamlessly whether you're in Tbilisi, Madrid, Istanbul, or Berlin.

---

## ✨ Key Features

### 👥 **Smart Student & Group Management**
- Detailed student profiles with subjects, schedules, and pricing
- Multi-student group support with per-lesson attendance tracking
- Quick search, filter, and inline updates
- Optional parent contact fields for direct communication

### 📅 **Intelligent Scheduling**
- Weekday-based calendar with infinite scrolling
- One-tap lesson creation with smart defaults
- Automatic reminders 1 hour before each lesson
- Per-student lesson notes and homework tracking

### 💬 **Parent Communication (NEW in v1.2)**
- **Direct WhatsApp & SMS messaging** with one tap
- Auto-generated, branded messages in the teacher's chosen language
- **Differential group notifications** — attending students' parents get one message, absent students' parents get another
- Lesson scheduled / canceled / rescheduled notifications
- Payment reminders for late-paying parents
- Subtle "Sent via Teacher Diary" branding for organic growth

### 💰 **Financial Tracking**
- Per-student pricing with multi-currency support
- Payment history and reminders
- Daily, weekly, and monthly earnings
- Visual charts powered by Williamchart

### 🌍 **Truly International**
- **7 fully localized languages**: English, ქართული (Georgian), Русский, Türkçe, Español, Português, Deutsch
- **International phone numbers** powered by Google's libphonenumber — auto-detects country from SIM
- **Per-app language** support on Android 13+ (system Settings integration)

### 🎨 **Modern, Polished UX**
- Material 3 design system
- Edge-to-edge layouts with adaptive theming
- Dark and light mode
- Smart UI hints (animated FAB for first-time actions)
- Onboarding flow for new teachers

### 🔐 **Privacy-First**
- All data stored **locally** on the device — no cloud collection
- Phone numbers normalized to E.164 standard
- Encrypted entitlement storage
- GDPR-compliant data handling

---

## 🌐 Supported Languages

| Flag | Language | Code | Status |
|------|----------|------|--------|
| 🇬🇧 | English | `en` | ✅ Complete |
| 🇬🇪 | ქართული | `ka` | ✅ Complete |
| 🇩🇪 | Deutsch | `de` | ✅ Complete |
| 🇹🇷 | Türkçe | `tr` | ✅ Complete |
| 🇷🇺 | Русский | `ru` | ✅ Complete |
| 🇪🇸 | Español | `es` | ✅ Complete |
| 🇵🇹 | Português | `pt` | ✅ Complete |

---

## 🛠 Tech Stack

### Core
- **Language:** Kotlin 2.0
- **UI:** Material 3, ViewBinding, ConstraintLayout
- **Architecture:** MVVM with Repository pattern
- **Min SDK:** 26 (Android 8.0) · **Target SDK:** 35 (Android 15)

### AndroidX & Jetpack
- **Database:** Room 2.8 (with manual migrations)
- **Lifecycle:** ViewModel + LiveData
- **Navigation:** Navigation Component
- **Coroutines:** kotlinx.coroutines for async work
- **Activity Result API** for permissions and flows

### Third-Party
- **Phone numbers:** [libphonenumber-android](https://github.com/MichaelRocks/libphonenumber-android) (Google's i18n library, Android-optimized)
- **Charts:** [Williamchart](https://github.com/diogobernardino/WilliamChart)
- **Auth:** Firebase Authentication
- **Analytics:** Firebase Analytics + Facebook SDK
- **Billing:** Google Play Billing 7
- **JSON:** Gson

### Build & Tooling
- Gradle Kotlin DSL with Version Catalog (`libs.versions.toml`)
- AGP 8.4 · Kotlin 2.0
- ProGuard/R8 with code shrinking and resource optimization

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────┐
│                   UI LAYER                      │
│  Activities · Fragments · Adapters · Dialogs    │
└────────────────────┬────────────────────────────┘
                     │ observes / triggers
                     ▼
┌─────────────────────────────────────────────────┐
│                ViewModel Layer                  │
│      LiveData · Coroutines · Business Logic     │
└────────────────────┬────────────────────────────┘
                     │ delegates to
                     ▼
┌─────────────────────────────────────────────────┐
│            Repository (Single Source)           │
│   Centralized via MyApp · Suspend functions     │
└────────────────────┬────────────────────────────┘
                     │ accesses
                     ▼
┌─────────────────────────────────────────────────┐
│              Data Layer (Room DB)               │
│  DAOs · Entities · Migrations · TypeConverters  │
└─────────────────────────────────────────────────┘
```

**Key architectural decisions:**
- **Singleton repository** initialized at `Application.onCreate()` — no global state, no service locators
- **Reactive UI** via LiveData/Flow combinators (`MediatorLiveData` for cross-stream merging)
- **8 sequential migrations** with try/catch idempotency (production-safe upgrades)
- **Locale management** via `AppCompatDelegate` (Android 13+ per-app language compatible)
- **Parent notifications** decoupled into a single `ParentNotifier` object — easy to extend with new message types

---

## 📂 Project Structure

```
app/src/main/
├── java/com/giorgi/diaryofteachers/
│   ├── adapters/              ← RecyclerView adapters
│   ├── db/
│   │   ├── dao/               ← Room DAOs (Student, Group, Lesson, Payment, Earnings)
│   │   └── repository/        ← Repository + DiaryTeacherDatabase + Converters
│   ├── models/                ← Entity classes (data layer)
│   ├── notification/          ← ParentNotifier · ReminderUtils · LessonReminderReceiver
│   ├── payWall/               ← FeatureGate · BillingEntitlementSync · PaywallBottomSheet
│   ├── screens/
│   │   ├── addlesson/         ← Add/Edit lesson flows
│   │   ├── addstudent/        ← Add student form
│   │   ├── AddGroups/         ← Group creation
│   │   ├── base/              ← BaseActivity · MyApp (Application class)
│   │   ├── dailyStatistic/    ← Daily stats screen
│   │   ├── earnMoney/         ← Earnings dashboard
│   │   ├── languages/         ← Language picker + LocaleController
│   │   ├── listofstudents/    ← Student list
│   │   ├── listofgroups/      ← Group list
│   │   ├── onboarding/        ← First-launch tour
│   │   ├── payment/           ← Payment dialog
│   │   ├── profile/           ← User profile + Premium activation
│   │   ├── settings/          ← App settings + Theme manager
│   │   ├── statistic/         ← Weekly stats
│   │   ├── statisticMonth/    ← Monthly stats
│   │   ├── statisticStudent/  ← Per-student stats
│   │   └── weekDays/          ← Day fragments (Mon–Sun)
│   ├── utils/                 ← PhoneNumberUtil · FacebookEvents
│   ├── MainActivity.kt
│   └── SharedViewModel.kt
└── res/
    ├── layout/                ← XML layouts
    ├── drawable/              ← Vector icons & backgrounds
    ├── values/                ← Default strings (en) + colors + themes
    ├── values-ka/, values-ru/, values-tr/, values-es/, values-pt/, values-de/
    └── xml/locales_config.xml ← Per-app language config (Android 13+)
```

---

## 🚀 Roadmap

The following features are planned for upcoming releases:

- [ ] **Recurring lessons** — set up weekly/monthly schedules in seconds
- [ ] **Cloud backup** (Google Drive) — peace of mind for teachers
- [ ] **Year-end PDF certificates** — printable certificates with teacher signature
- [ ] **Make-up lesson tracker** — credit system for missed lessons
- [ ] **Voice memos & photo notes** per lesson
- [ ] **Income forecasting** — visualize next month's projected earnings
- [ ] **Birthday reminders** for students with one-tap greetings
- [ ] **Multi-device sync** for teachers using both phone and tablet
- [ ] **Excel/CSV export** for tax season

---

## 🎓 What Makes This Project Stand Out

This isn't just another CRUD app. Some highlights from the engineering side:

- **🌍 Real internationalization** — not just translated strings, but country-aware phone formatting, per-app language settings, and culturally appropriate UX patterns
- **📞 Production-grade phone handling** — Google's libphonenumber with SIM auto-detection, validation, and E.164 normalization
- **🔄 Safe schema evolution** — 8 sequential Room migrations with idempotency guarantees
- **🎨 Polished UX details** — animated hints, smart defaults, toast feedback, snackbar anchoring
- **♻️ Backwards compatibility** — supports Android 8.0 (API 26) through Android 15 (API 35)
- **🏗 Clean architecture** — testable repositories, single source of truth, no leaky abstractions

---

## 👨‍💻 About the Developer

I'm **Giorgi**, an Android developer passionate about crafting polished, user-centric mobile experiences. Teacher Diary is a project I've poured countless hours into — not just to ship features, but to think deeply about what makes an app *delightful* for its users.

I specialize in:

- **Native Android development** with Kotlin & Jetpack
- **Material 3** design implementation
- **Multilingual & internationalized** apps for global markets
- **Room database** design and migration management
- **Third-party integrations** (Firebase, Facebook SDK, Google Play Billing, libphonenumber)
- **End-to-end app delivery** — from concept to Play Store release

### 💼 Available for Hire

I'm available for **freelance Android projects** on Upwork. If you need:

- A **new Android app** built from scratch
- An **existing app modernized** (Kotlin migration, Material 3 redesign, internationalization)
- **Specific features** added (in-app billing, push notifications, multi-language support)
- **Technical consulting** for your Android team

…let's talk!

📧 **Email:** giorgilatsabidze84@gmail.com
🔗 **Upwork:** [Profile link]
📱 **Portfolio:** This project + others on my GitHub

---

## 📄 License

Copyright © 2026 Giorgi. All rights reserved.

This is a commercial product. Source code is available for review purposes only and may not be redistributed without permission.

---

<div align="center">

**Built with ❤️ for teachers around the world.**

If you find this project interesting, give it a ⭐ on GitHub!

</div>
