# SafeLink - Campus Safety & Emergency Alert System

![SafeLink Logo](assets/images/splash_logo.png)

> A real-time safety and emergency alert system for NSTU (Noakhali Science and Technology University) campus designed to provide instant communication between students, proctors, and staff during emergencies.

---

## 📱 Overview

SafeLink is a comprehensive mobile application developed for campus safety management. The app enables students to quickly report emergencies, share their real-time GPS location, and receive instant alerts through a multi-tiered escalation system. Staff and proctors can monitor incidents in real-time and take immediate action.

**Status:** Active Development | **Platform:** Flutter (iOS, Android, Web) | **Backend:** Firebase

---

## ✨ Key Features

### For Students:
- 🆘 **One-Tap Emergency Alert** - Quick distress signal reporting
- 📍 **Real-Time GPS Tracking** - Automatic location sharing with emergency responders
- 🔔 **Instant Notifications** - Real-time updates on alert status
- 👥 **Multiple Proctors** - Send emergency SMS to multiple registered proctors
- 🔐 **Secure Authentication** - Phone OTP-based login system
- 📞 **Direct Contact** - Quick access to emergency contacts

### For Staff & Proctors:
- 📊 **Real-Time Dashboard** - View active emergency alerts with location
- 🗺️ **Live GPS Tracking** - Monitor student locations during emergencies
- ⚡ **Escalation Workflow** - Multi-level alert escalation system
- 📱 **SMS Notifications** - SMS and in-app alerts for new incidents
- ✅ **Incident Management** - Update and close emergency reports
- 📈 **Analytics & Reports** - Track incidents and response metrics

---

## 🛠️ Tech Stack

### Frontend:
- **Flutter** - Cross-platform mobile framework (iOS, Android, Web)
- **Dart** - Programming language
- **Provider** - State management
- **GetX** - Navigation and reactive programming
- **Firebase** - Backend services

### Backend & Services:
- **Firebase Firestore** - Real-time database
- **Firebase Authentication** - OTP-based auth
- **Firebase Cloud Functions** - Serverless backend
- **Firebase Cloud Messaging (FCM)** - Push notifications
- **Firebase Storage** - File storage
- **Twilio SDK** - SMS notifications

### External Services:
- **Google Maps API** - GPS tracking and mapping
- **Twilio** - Multi-channel messaging

---

## 📋 Prerequisites

Before running the project, ensure you have:

- **Flutter SDK** (v3.0 or higher)
- **Dart SDK** (v2.18 or higher)
- **Android Studio** (for Android development)
- **Xcode** (for iOS development on macOS)
- **Firebase Project** (created and configured)
- **Google Maps API Key**
- **Twilio Account** (for SMS functionality)

---

## 🚀 Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/Jukta06/SafeLink-NSTU.git
cd SafeLink-NSTU
```

### 2. Install Dependencies

```bash
flutter clean
flutter pub get
```

### 3. Firebase Configuration

#### Android:
1. Download `google-services.json` from Firebase Console
2. Place it in `android/app/`
3. Update `android/build.gradle.kts` with your Firebase project details

#### iOS:
1. Download `GoogleService-Info.plist` from Firebase Console
2. Place it in `ios/Runner/`
3. Open `ios/Podfile` and run:
   ```bash
   cd ios && pod install && cd ..
   ```

#### Web:
1. Configure Firebase for web in `lib/firebase_options.dart`

### 4. API Keys Configuration

Create a file `lib/config/secrets.dart`:

```dart
class AppSecrets {
  static const String googleMapsApiKey = 'YOUR_GOOGLE_MAPS_API_KEY';
  static const String twilioAccountSid = 'YOUR_TWILIO_ACCOUNT_SID';
  static const String twilioAuthToken = 'YOUR_TWILIO_AUTH_TOKEN';
  static const String twilioPhoneNumber = 'YOUR_TWILIO_PHONE_NUMBER';
}
```

### 5. Firebase Firestore Setup

Initialize your Firestore database with the following structure:

```
users/
  {userId}/
    - email: string
    - phone: string
    - name: string
    - role: string (student/proctor/staff)
    - registeredProctors: array
    - createdAt: timestamp

emergencyAlerts/
  {alertId}/
    - studentId: string
    - studentName: string
    - location: GeoPoint
    - status: string (active/resolved/escalated)
    - timestamp: timestamp
    - description: string
    - assignedProctor: string

proctors/
  {proctorId}/
    - name: string
    - phone: string
    - email: string
    - campus: string
    - activeAlerts: array
    - createdAt: timestamp
```

### 6. Enable Firebase Features

In Firebase Console:
- ✅ Enable Firestore Database
- ✅ Enable Authentication (Phone)
- ✅ Enable Cloud Functions
- ✅ Enable Cloud Messaging (FCM)
- ✅ Set up Firestore Security Rules

---

## 🏃 Running the Application

### Development Mode:

```bash
# Run on connected device/emulator
flutter run

# Run with specific device
flutter run -d <device_id>

# Run in release mode
flutter run --release
```

### Web:

```bash
flutter run -d web
```

### Build APK (Android):

```bash
flutter build apk --release
```

### Build IPA (iOS):

```bash
flutter build ios --release
```

---

## 📁 Project Structure

```
lib/
├── main.dart                      # App entry point
├── firebase_options.dart          # Firebase configuration
├── config/
│   ├── routes.dart                # App routing
│   └── theme.dart                 # UI theme configuration
├── core/
│   ├── errors/
│   ├── utils/
│   └── widgets/                   # Reusable widgets
├── data/
│   ├── models/                    # Data models
│   ├── repositories/              # Repository pattern
│   └── services/
│       ├── firebase_service.dart
│       ├── location_service.dart
│       └── notification_service.dart
├── domain/
│   ├── entities/                  # Business logic entities
│   └── use_cases/
├── presentation/
│   ├── pages/                     # Screen pages
│   ├── providers/                 # State management (Provider/GetX)
│   └── widgets/                   # UI components
└── functions/                     # Firebase Cloud Functions

android/                           # Android configuration
ios/                              # iOS configuration
web/                              # Web configuration
functions/                         # Firebase Cloud Functions (Node.js)
docs/                             # Documentation
```

---

## 🔒 Firestore Security Rules

Apply these security rules in Firestore Console:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Users collection - only own data
    match /users/{userId} {
      allow read, write: if request.auth.uid == userId;
    }
    
    // Emergency alerts - students create, proctors read
    match /emergencyAlerts/{alertId} {
      allow create: if request.auth.uid != null;
      allow read: if request.auth.uid != null;
      allow update: if request.auth.uid != null;
    }
    
    // Proctors collection - public read, own write
    match /proctors/{proctorId} {
      allow read: if true;
      allow write: if request.auth.uid == proctorId;
    }
  }
}
```

---

## 🔄 Firebase Cloud Functions

Deploy backend functions:

```bash
cd functions
npm install
firebase deploy --only functions
```

**Key Functions:**
- `sendAlertNotification()` - Sends SMS to proctors
- `escalateAlert()` - Multi-tier alert escalation
- `createUser()` - User initialization on signup
- `updateLocation()` - Real-time location updates

---

## 📞 SMS Gateway Integration (Twilio)

1. Sign up for [Twilio](https://www.twilio.com/)
2. Get Account SID, Auth Token, and Phone Number
3. Configure in Firebase Cloud Functions:
   ```bash
   firebase functions:config:set twilio.account_sid="YOUR_SID"
   firebase functions:config:set twilio.auth_token="YOUR_TOKEN"
   firebase functions:config:set twilio.phone_number="YOUR_NUMBER"
   ```

---

## 🧪 Testing

Run tests:

```bash
flutter test
```

Test specific file:

```bash
flutter test test/widget_test.dart
```

---

## 🐛 Troubleshooting

### Firebase Connection Issues:
- Verify `google-services.json` and `GoogleService-Info.plist` are in correct locations
- Check Firebase project ID matches in `firebase.json`
- Ensure Firebase project is active in Console

### GPS Not Working:
- Grant location permissions on device
- Ensure Google Maps API key is correctly set
- Check location service is enabled on device

### SMS Not Sending:
- Verify Twilio credentials
- Check Twilio account has sufficient credits
- Verify phone numbers are in correct format

### Firestore Rules Error:
- Check user is authenticated
- Verify user ID matches Firestore document
- Review Firestore Security Rules in Console

---

## 🚀 Deployment

### Firebase Hosting (Web):

```bash
flutter build web --release
firebase deploy --only hosting
```

### App Store (iOS):

1. Create App Store Connect application
2. Configure signing certificates
3. Build and upload with Xcode

### Google Play Store (Android):

1. Create Google Play Console application
2. Generate signed APK/AAB
3. Upload to Play Console

---

## 📚 Documentation

- [Firebase Setup Guide](docs/FIREBASE_FUNCTIONS.md)
- [Escalation Workflow](docs/OPTIMIZED_ESCALATION_WORKFLOW.md)
- [GPS Implementation](docs/REALTIME_GPS_FIX_PLAN.md)
- [Project Documentation](docs/SafeLink_NSTU_Project_Documentation.md)

---

## 👥 Contributing

We welcome contributions! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/YourFeature`)
3. Commit changes (`git commit -m 'Add YourFeature'`)
4. Push to branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

---

## 📞 Support & Contact

For issues, questions, or feature requests:

- **GitHub Issues:** [SafeLink Issues](https://github.com/Jukta06/SafeLink-NSTU/issues)
- **Email:** safelink.nstu@example.com
- **Campus:** Noakhali Science and Technology University (NSTU)

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🎓 Acknowledgments

- NSTU Administration & Campus Management
- Firebase & Google Cloud Services
- Flutter Community
- Twilio Communications API

---

## 🗺️ Roadmap

- ✅ Real-time GPS tracking
- ✅ Multi-proctor SMS alerts
- ✅ Emergency escalation workflow
- 🔄 **In Progress:** Advanced analytics dashboard
- 📋 **Planned:** Offline mode support
- 📋 **Planned:** Video call integration
- 📋 **Planned:** AI-powered incident prediction

---

**Last Updated:** March 2026 | **Version:** 1.0.0 | **Status:** Active Development

---

*SafeLink - Making Campus Safer Together* 🛡️
