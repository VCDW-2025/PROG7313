# 🔄 **Activity Life Cycle**

The **Activity Life Cycle** is a core concept in Android development. It defines how your app behaves as users **open**, **pause**, **resume**, **rotate**, or **close** an activity (screen). Understanding it helps you manage app state, resources, and user experience correctly.

---

## 🪁 **What is an Activity?**
An **Activity** is a single screen in your app. Think of it like a page in a book. 
Android manages its lifecycle through predefined **callback methods**.

---

## 🧩 **The Lifecycle Methods**


| Method         | Triggered When... |
|----------------|-------------------|
| `onCreate()`   | Activity is **first created** – used for initial setup (UI, listeners, etc.) |
| `onStart()`    | Activity is becoming **visible** |
| `onResume()`   | Activity is now **in the foreground** and interactive |
| `onPause()`    | Another activity comes in front – pause heavy tasks (e.g., video, location) |
| `onStop()`     | Activity is **no longer visible** |
| `onRestart()`  | Called if activity is restarting from stopped state |
| `onDestroy()`  | Activity is about to be **destroyed** – cleanup memory, close connections |

---

## 🌊 **Lifecycle Flow Diagram**

Typical full cycle:

```
onCreate() → onStart() → onResume()
→ [User navigates away]
→ onPause() → onStop()
→ [User comes back]
→ onRestart() → onStart() → onResume()
→ [App is closed]
→ onPause() → onStop() → onDestroy()
```

---

### ⚙️ **Example: Logging Lifecycle**

```kotlin
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    Log.d("LIFECYCLE", "onCreate called")
}

override fun onStart() {
    super.onStart()
    Log.d("LIFECYCLE", "onStart called")
}

override fun onResume() {
    super.onResume()
    Log.d("LIFECYCLE", "onResume called")
}

override fun onPause() {
    super.onPause()
    Log.d("LIFECYCLE", "onPause called")
}

override fun onStop() {
    super.onStop()
    Log.d("LIFECYCLE", "onStop called")
}

override fun onDestroy() {
    super.onDestroy()
    Log.d("LIFECYCLE", "onDestroy called")
}
```

Use **Logcat** in Android Studio to view the output when your activity goes through different states.

---

### 🎯 Why It Matters:
- Helps you save/restore user data
- Prevents memory leaks by releasing resources
- Improves app performance and user experience




