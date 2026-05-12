# 🔦 LightWidget

An Android home screen widget that toggles the device flashlight with a single tap — no need to open any app.

## ✨ Features

- 💡 **One-tap flashlight toggle** directly from the home screen widget
- 🏠 **No app to open** — works entirely as a home screen widget via `AppWidgetProvider`
- 🌙 **Dark mode support** — widget colors adapt to system theme via custom style attributes
- 📐 **Resizable widget** — supports horizontal and vertical resizing on the home screen
- 💾 **State persistence** — flashlight state is saved across widget updates using `SharedPreferences`

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Language | Kotlin |
| Framework | Android SDK (AppWidget API) |
| Flashlight | Camera2 API (`CameraManager.setTorchMode`) |
| State | SharedPreferences |
| UI | RemoteViews |
| Min SDK | API 16 (Android 4.1+) |
| Target SDK | API 30 (Android 11) |

## 🏗️ How It Works

This project demonstrates several non-trivial Android concepts working together:

**Widget lifecycle** — `LightWidget` extends `AppWidgetProvider` (a `BroadcastReceiver` subclass). On each update, it builds a `RemoteViews` layout and attaches a `PendingIntent` to the button that broadcasts a custom `toggleFlashlight` action.

**Toggle logic** — `onReceive` catches the custom broadcast, reads the current on/off state from `SharedPreferences`, flips it, and calls `CameraManager.setTorchMode()` from the **Camera2 API** to switch the flashlight.

**Theme support** — the widget layout uses custom `attrs.xml` attributes (`appWidgetBackgroundColor`, `appWidgetTextColor`) resolved at runtime, giving automatic light/dark mode adaptation.

```
LightWidget-master/
└── app/src/main/
    ├── java/com/example/widget/
    │   └── LightWidget.kt           # AppWidgetProvider: full toggle logic
    ├── res/
    │   ├── layout/light_widget.xml  # RemoteViews layout
    │   ├── xml/light_widget_info.xml# Widget metadata (size, update interval)
    │   └── values/attrs.xml         # Custom theme attributes for dark mode
    └── AndroidManifest.xml          # Widget receiver registration
```

## 🚀 Getting Started

### Prerequisites

- Android Studio Arctic Fox or newer
- A physical Android device (emulators don't have a flashlight)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/NackBard/LightWidget.git
   ```

2. Open the project in Android Studio and run it on a physical device.

3. Long-press your home screen → **Widgets** → find **LightWidget** → drag it to the home screen.

4. Tap the widget to toggle the flashlight on/off.

---

> Built with ❤️ using Kotlin, Camera2 API and Android AppWidget API
