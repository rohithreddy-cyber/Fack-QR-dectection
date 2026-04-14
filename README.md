# SecureQR: Intelligent QR Threat Detection & Payment Safety Application

> A Flutter-based Android application that scans QR codes and intelligently analyzes them to detect potential security threats such as phishing links, suspicious UPI IDs, and unsafe redirections before allowing any user action like payment.

---

## 📱 Features

### Core Features
- **Camera QR Scanning** — Real-time QR code scanning using device camera
- **Gallery Upload** — Scan QR codes from images in gallery
- **Content Decoding** — Decode text, URL, and UPI payment links

### 🧠 Threat Detection Engine
Rule-based intelligent system with **14+ detection rules**:
- 🔴 **Malicious URLs**: HTTP detection, suspicious domains, phishing keywords
- 🔴 **Phishing Patterns**: Typosquatting, IP address URLs, excessive subdomains
- 🟡 **Suspicious UPI IDs**: Random/meaningless IDs (entropy analysis), missing merchant name
- 🔴 **Hidden Redirections**: URL shortener detection
- 🟡 **Unknown Data**: Unrecognized formats, incomplete data

### 📊 Risk Scoring System
| Rule | Score Impact |
|------|-------------|
| Valid UPI format (upi://pay) | +50 |
| HTTPS secure connection | +30 |
| Merchant name present | +20 |
| Valid UPI ID (@ symbol) | +20 |
| Trusted domain | +20 |
| Insecure HTTP URL | -40 |
| IP address URL | -35 |
| Suspicious keywords | -30 |
| Random UPI ID pattern | -30 |
| URL shortener/redirect | -25 |
| Typosquatting | -25 |
| Missing merchant name | -20 |

### Classification
- 🟢 **SAFE** (Score > 70) — No threats detected, safe to proceed
- 🟡 **WARNING** (Score 40–70) — Suspicious, proceed with caution
- 🔴 **DANGEROUS** (Score < 40) — Threat detected, payment blocked

### 💳 Simulated Payment System
- Payment confirmation screen with merchant details
- Success animation with confetti effects
- Transaction history saved locally

### 📦 Additional Features
- SQLite-based scan history with persistence
- Swipe-to-delete and clear all history
- Detailed threat detection reasons with score breakdown

---

## 🏗️ Project Structure

```
secure_qr/
├── lib/
│   ├── main.dart                          # App entry point
│   ├── app.dart                           # MaterialApp + Routes
│   ├── theme/
│   │   ├── app_colors.dart                # Color palette & gradients
│   │   └── app_theme.dart                 # ThemeData & typography
│   ├── models/
│   │   ├── qr_scan_result.dart            # QR data model
│   │   ├── threat_analysis.dart           # Threat analysis model
│   │   └── scan_history_item.dart         # History persistence model
│   ├── services/
│   │   ├── qr_decoder_service.dart        # QR content parser
│   │   ├── threat_detection_service.dart   # Core threat engine
│   │   ├── database_service.dart          # SQLite operations
│   │   └── payment_service.dart           # Simulated payments
│   ├── screens/
│   │   ├── splash_screen.dart             # Animated splash
│   │   ├── home_screen.dart               # Main screen
│   │   ├── scanner_screen.dart            # Camera scanner
│   │   ├── result_screen.dart             # Analysis results
│   │   ├── payment_screen.dart            # Payment confirmation
│   │   ├── success_screen.dart            # Payment success
│   │   ├── blocked_screen.dart            # Threat blocked
│   │   └── history_screen.dart            # Scan history
│   ├── widgets/
│   │   ├── risk_meter.dart                # Circular risk gauge
│   │   ├── threat_card.dart               # Threat reason card
│   │   ├── scan_option_card.dart          # Home screen cards
│   │   ├── animated_shield.dart           # Pulsing shield icon
│   │   ├── gradient_button.dart           # Gradient button
│   │   ├── loading_overlay.dart           # Analysis overlay
│   │   └── history_tile.dart              # History list item
│   └── utils/
│       ├── constants.dart                 # App constants
│       └── validators.dart                # Validation helpers
├── android/                               # Android configuration
├── assets/
│   ├── animations/                        # Lottie files (optional)
│   └── images/                            # App images
└── pubspec.yaml                           # Dependencies
```

---

## 🚀 Setup Instructions

### Prerequisites

1. **Install Flutter SDK** (version 3.7.0 or higher):
   - Download from: https://docs.flutter.dev/get-started/install/windows
   - Extract to a folder (e.g., `C:\flutter`)
   - Add `C:\flutter\bin` to your system PATH

2. **Install Android Studio**:
   - Download from: https://developer.android.com/studio
   - Install Android SDK (API 34 or higher)
   - Set up an Android emulator or connect a physical device

3. **Install Git**:
   - Download from: https://git-scm.com/downloads

### Step-by-Step Setup

```bash
# 1. Verify Flutter is installed
flutter --version

# 2. Check all dependencies are met
flutter doctor

# 3. Navigate to the project directory
cd "c:\Users\rohit\Desktop\fack qrdection"

# 4. Get all dependencies
flutter pub get

# 5. Run on connected device or emulator
flutter run

# 6. Build APK (for sharing)
flutter build apk --release
```

### If `flutter create` was not run

Since this project was created manually, you may need to initialize the Flutter project structure:

```bash
# Navigate to the project folder
cd "c:\Users\rohit\Desktop\fack qrdection"

# Create a new Flutter project in a temporary folder
flutter create --org com.secureqr --platforms=android temp_project

# Copy missing files from temp_project to your project:
# - android/app/src/main/res/mipmap-* (app icons)
# - android/app/src/debug/AndroidManifest.xml
# - android/app/src/profile/AndroidManifest.xml
# - android/app/proguard-rules.pro
# - .metadata
# - .gitignore

# Then copy the generated local.properties
copy temp_project\android\local.properties android\local.properties

# Delete the temporary project
rmdir /s temp_project

# Now get dependencies and run
flutter pub get
flutter run
```

### Quick Alternative Setup

```bash
# 1. Create a fresh Flutter project
flutter create --org com.secureqr --platforms=android secure_qr_temp

# 2. Copy the lib/ folder, pubspec.yaml, and assets/ from this project
#    into the newly created secure_qr_temp project

# 3. Copy android/app/src/main/AndroidManifest.xml to replace the
#    generated one (to include camera permissions)

# 4. Get dependencies and run
cd secure_qr_temp
flutter pub get
flutter run
```

---

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `mobile_scanner` | ^7.0.0 | QR code camera scanning |
| `image_picker` | ^1.2.1 | Gallery image selection |
| `sqflite` | ^2.4.2 | Local SQLite database |
| `path_provider` | ^2.1.5 | File system paths |
| `google_fonts` | ^6.2.1 | Typography (Inter, Outfit) |
| `provider` | ^6.1.2 | State management |
| `intl` | ^0.19.0 | Date formatting |
| `url_launcher` | ^6.3.1 | External URLs |
| `percent_indicator` | ^4.2.4 | Risk meter gauge |
| `flutter_animate` | ^4.5.2 | Animations |

---

## 🎨 Design

- **Dark Theme** — Deep navy (#0A0E21) with gradient overlays
- **Glassmorphism** — Frosted glass cards with subtle borders
- **Accent Colors** — Cyan (#00D4FF) and Purple (#7B61FF) gradients
- **Status Colors** — Green (Safe), Amber (Warning), Red (Danger)
- **Typography** — Outfit for headings, Inter for body text
- **Animations** — Pulse effects, counting animations, confetti

---

## 🧪 Test QR Codes

Use these sample QR data strings for testing:

| QR Data | Expected Result |
|---------|----------------|
| `upi://pay?pa=merchant@upi&pn=ShopName&am=100&cu=INR` | 🟢 SAFE |
| `upi://pay?pa=x7hd82@upi` | 🔴 DANGEROUS |
| `https://www.google.com` | 🟢 SAFE |
| `http://free-reward-login.xyz/verify` | 🔴 DANGEROUS |
| `https://bit.ly/abc123` | 🟡 WARNING |
| `Hello World` | 🟢 SAFE (plain text) |

---

## 📄 License

This project is developed for academic purposes as a final-year BTech project.

---

## 👨‍💻 Author

Developed as part of BTech Final Year Project — **SecureQR: Intelligent QR Threat Detection & Payment Safety Application**
