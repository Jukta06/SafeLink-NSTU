# SafeLink NSTU

SafeLink NSTU is a mobile-first Women Safety SOS system designed to provide fast emergency support during critical situations. Users can trigger SOS alerts, share live location and notify relevant responders instantly through a simple and reliable interface.

## 🚨 Problem Statement
The current system for reporting and responding to student emergencies at Noakhali Science and Technology University (NSTU) is entirely manual, leading to serious inefficiencies and delays in critical situations. When emergencies such as ragging, harassment, or other incidents occur, students have to contact Teachers, Proctor Office or call them directly, a process that is slow and unreliable. There is no centralized platform to collect incident information, verify users, track alerts, or maintain accountability of responses. This lack of a streamlined system creates confusion about who should respond, increases response times, and lowers students’ confidence in campus safety.
SafeLink NSTU solves this by enabling one-tap SOS activation with real-time location and alert updates.

## 💡 Solution Overview
SafeLink NSTU offers a fast and user-friendly safety workflow that allows users to:

- Trigger SOS alerts instantly
- Share live location in real time
- Notify responders through cloud-backed alert flows
- Track and control alert status
- Cancel alerts when the situation is safe
- The system is built for real-time performance and future scalability.

## ✨ Features
- One-tap SOS activation: Instantly send an emergency alert with a single tap.
- Real-time live location sharing: Captures and updates the user’s current location.
- Firebase-powered live backend sync: Alert events and status changes are updated instantly.
- Emergency contact escalation support: Supports SMS/call based escalation workflows.
- Alert status monitoring and cancel control: Users can monitor and cancel active SOS alerts.
- Multi-role dashboard support: Includes role-based flows such as student/proctor/security views.
- Shake-trigger integration: Optional shake-based trigger support for quick emergency activation.
- Volume button emergency trigger: Quick SOS activation using physical volume button press for hands-free operation.
## 🛠️ Technologies Used
- Frontend app development: Flutter (Dart)
- Backend services: Firebase (Cloud Firestore, Authentication, Cloud Functions, Messaging)
- Real-time alert and status updates: Firebase services
- Location services: Geolocator + Geocoding
- Map and location visualization: Google Maps Flutter
- Notification handling: Firebase Messaging + Flutter Local Notifications
## 📊 System Workflow
- User triggers SOS from the app
- System captures current location
- Alert data is sent to Firebase in real time
- Emergency status and location updates are synced instantly
- Responders can process/accept/reject alerts
- User can cancel SOS alert to prevent false alarm.
## Local Development Setup
Prerequisites
- Flutter SDK installed
- Dart SDK (comes with Flutter)
- Node.js 18+ (for functions)
- Firebase CLI 
1) Clone and install Flutter dependencies
git clone https://github.com/Jukta06/SafeLink-NSTU.git
cd SafeLink-NSTU
flutter pub get
2) Run the app
flutter run
Examples:

flutter run -d chrome
3) Setup and run Cloud Functions locally
cd functions
npm install
npm run start
4) Deploy Cloud Functions
cd functions
npm run deploy
Environment and Secrets

## Apk file
Download link: https://github.com/Jukta06/SafeLink-NSTU/releases/tag/Apk_file
