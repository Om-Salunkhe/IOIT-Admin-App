# IOIT College Admin App

An Android app for college admins to publish notices and gallery images to the [IOIT College App](https://github.com/Om-Salunkhe/IOIT-College-App). Everything an admin uploads here is stored in Firebase and shows up in the student app.

## Features

- **Upload notice:** pick an image from the device, add a title, and publish.
  - The image goes to Firebase Storage under `Notice/`.
  - The notice (title, image URL, date and time) is written to the Realtime Database under `Notice/`.
- **Upload gallery image:** pick an image and a category.
  - The image goes to Firebase Storage under `gallery/`.
  - Its download URL is saved in the Realtime Database under `gallery/<category>`.

## How it fits together

```
IOIT Admin App ──uploads──▶ Firebase Storage  (Notice/, gallery/)
               ──writes───▶ Firebase Realtime Database (Notice/, gallery/<category>)
                                         │
IOIT College App ◀──────reads────────────┘
```

Both apps share one Firebase project.

## Tech stack

- Java, Android SDK (min SDK 21, target SDK 33)
- Firebase Realtime Database, Firebase Storage, Firebase Analytics
- Material Components, ConstraintLayout
- Gradle

## Project structure

```
app/src/main/java/com/example/juetadmin/
  MainActivity.java   home screen with "Upload Notice" and "Upload Image" actions
  add_notice.java     notice upload flow
  Uploadimage.java    gallery upload flow with category picker
  NoticeData.java     notice model written to the database
```

## Getting started

1. Clone the repo and open it in Android Studio.
2. Connect it to your own Firebase project:
   - create an Android app in the Firebase console with package name `com.example.juetadmin`;
   - download `google-services.json` and replace `app/google-services.json`;
   - enable Realtime Database and Storage.
3. Let Gradle sync, then run on a device or emulator (Android 5.0+).

To see uploads in the student app, point the [IOIT College App](https://github.com/Om-Salunkhe/IOIT-College-App) at the same Firebase project.

## Notes

- The app has no login screen, so anyone with the APK can publish. Lock this down with Firebase Authentication and Realtime Database and Storage security rules before real use.
- The app needs storage permission to pick images.
