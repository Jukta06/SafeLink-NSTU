# SafeLink NSTU

SafeLink NSTU is a Flutter-based campus safety application with Firebase backend services and a Firebase Cloud Functions module.

This README is intentionally based on files that currently exist in this repository so setup information stays accurate.

## Repository

- URL: https://github.com/Jukta06/SafeLink-NSTU
- Flutter app package name: `safelink_n`
- App version: `1.0.0+1`

## Verified Tech Stack

### Mobile/Web app

- Flutter (Dart, SDK constraint `^3.9.2`)
- Firebase: `firebase_core`, `firebase_auth`, `cloud_firestore`, `firebase_messaging`, `cloud_functions`
- Location/Map: `geolocator`, `geocoding`, `google_maps_flutter`
- Notifications: `flutter_local_notifications`
- Device interaction: `permission_handler`, `sensors_plus`, `shake`, `volume_controller`
- UI/utility: `google_fonts`, `shared_preferences`, `url_launcher`

### Cloud Functions (`functions`)

- Runtime: Node.js `>=18`
- Main libraries: `firebase-admin`, `firebase-functions`, `@sendgrid/mail`, `twilio`, `@google-cloud/tasks`

## Verified Firebase Configuration In Repo

- `firebase.json` configures:
  - Firestore rules file: `firestore.rules`
  - Functions source directory: `functions`
  - Emulator ports: Functions `5001`, Firestore `8080`, UI `4000`
- `lib/firebase_options.dart` is present and includes Firebase options for Web, Android, and Windows targets.
- Firestore rules are stored in `firestore.rules`.

## Main App Structure

Top-level Flutter source structure:

- `lib/main.dart`
- `lib/presentation`
- `lib/core`
- `lib/data`
- `lib/domain`
- `lib/config`
- `lib/firebase_options.dart`

Platform folders present:

- `android`
- `ios`
- `web`
- `windows`
- `linux`
- `macos`

Backend and docs:

- `functions`
- `docs`

## Notable Implemented Modules (From Source Files)

The repository currently includes code for:

- Auth screens and controllers (`login`, `signup`, `email verification`, `forgot password`, `profile setup`)
- Home and alert-related screens (`alerts`, `alert detail`, `notification details`)
- Role-specific screens (`proctor dashboard`, `proctorial dashboard`, `security dashboard`)
- Location/map and SOS-related services (location service, shake detection, SMS/call escalation services)
- Theme and route management

## Cloud Functions Exports (From `functions/index.js`)

Current exported functions include:

- `requestOtp` (callable)
- `sendSignupOtpEmail` (Firestore trigger)
- `sendSosAlert` (HTTP)
- `acceptAlert` (HTTP)
- `rejectAlert` (HTTP)
- `getPendingAlerts` (HTTP)
- `getAllAlerts` (HTTP)
- `sendShakeAlertSMS` (callable)
- `processEscalationSMS` (HTTP)
- `processEscalationCall` (HTTP)

## Local Development Setup

### Prerequisites

- Flutter SDK installed
- Dart SDK (comes with Flutter)
- Node.js 18+ (for `functions`)
- Firebase CLI (for emulator/deploy workflows)

### 1) Clone and install Flutter dependencies

```bash
git clone https://github.com/Jukta06/SafeLink-NSTU.git
cd SafeLink-NSTU
flutter pub get
```

### 2) Run the app

```bash
flutter run
```

Examples:

```bash
flutter run -d chrome
flutter run -d windows
```

### 3) Setup and run Cloud Functions locally

```bash
cd functions
npm install
npm run start
```

### 4) Deploy Cloud Functions

```bash
cd functions
npm run deploy
```

## Environment and Secrets

This repository expects sensitive credentials via environment/config variables for services such as SendGrid and Twilio in the Cloud Functions runtime.

Do not commit secrets to Git.

## Testing

Run Flutter tests:

```bash
flutter test
```

## Documentation

Additional project documents are available in `docs/`, including:

- `FIREBASE_FUNCTIONS.md`
- `OPTIMIZED_ESCALATION_WORKFLOW.md`
- `PERSISTENT_LOGIN_IMPLEMENTATION.md`
- `REALTIME_GPS_FIX_PLAN.md`
- `SHAKE_ALERT_ESCALATION_SPEC.md`
- `SHAKE_SERVICE_INTEGRATION.md`
- `SMS_TO_MULTIPLE_PROCTORS_PLAN.md`
- `SafeLink_NSTU_Project_Documentation.md`


