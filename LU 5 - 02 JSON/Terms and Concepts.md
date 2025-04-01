### 🧠 Concepts
| Concept | Kotlin Code | Explanation |
|--------|--------------|-------------|
| **Serialisation** | Gson().toJson(object) | Convert object to JSON string |
| **Deserialisation** | Gson().fromJson(json, Class) | Convert JSON string to object |
| **Reading JSON** | From assets or API | Use BufferedReader and Gson |
| **Writing JSON** | To SharedPreferences | Save using putString() |

---

# ✅ `println()` vs `Log.d()`

| Feature                | `println()`                            | `Log.d()` (or `Log.i`, `Log.e`)                      |
|------------------------|----------------------------------------|------------------------------------------------------|
| Where output appears   | Sometimes in **Run** tab only           | In the **Logcat window** (Android's main debug tool) |
| Filtering              | ❌ Cannot filter by tag or severity     | ✅ Can filter by tag (e.g., `"JSON_TEST"`) or level   |
| Level of control       | ❌ None                                 | ✅ Debug (`d`), Info (`i`), Warning (`w`), Error (`e`) |
| Professional practice  | ❌ Not used in production apps          | ✅ Standard debugging method in Android development   |
| Contextual tags        | ❌ No tagging                          | ✅ Custom tags help trace logs easily                |

---

### 📲 Example in Android

```kotlin
import android.util.Log

val jsonString = Gson().toJson(order)
Log.d("JSON_TEST", "Serialized JSON: $jsonString")
```

- `"JSON_TEST"` is a **tag** — you can filter Logcat to only show these logs.
- `"Serialised JSON: ..."` is the message — you can include variable values, status messages, or debugging clues.

---

### 💡 Why It Matters in Class and IRL

- ✅ **Learn proper tools** used in real-world Android development.
- ✅ **Logcat** is what developers, testers, and QA teams use to debug issues.
- ✅ Logs can be filtered to find errors quickly — essential in large projects.
- ✅ It helps you separate logs by purpose (`d` for debug, `e` for errors, etc.).

---

### 🧪 Pro Tip:

Use different log levels:
```kotlin
Log.d("TAG", "Debugging info")
Log.i("TAG", "Just an update")
Log.w("TAG", "Something might be wrong")
Log.e("TAG", "Something went wrong")
```

---

# 🗂️ **1. Android Pane (Simplified View)**

- This is the **default view** in Android Studio.
- Organises files in a **logical, Android-specific way** — not by actual folder structure.
- Shows folders like:
  - `manifests/`
  - `java/`
  - `res/` (for layouts, drawables, values)
- Hides things like `build`, `src`, and `assets` unless you dig deeper.

✅ **Best for:** Beginners and app developers focusing on UI and logic, not on file system structure.

---

# 📁 **2. Project Pane (True File Structure)**

- Shows your app **exactly as it is stored on disk**.
- You'll see folders like:
  ```
  app/
    ├─ build/
    ├─ src/
        ├─ main/
            ├─ java/
            ├─ res/
            ├─ assets/
  ```
- You can **create new folders** (like `assets/`, `raw/`, `data/`, etc.) more easily here.

✅ **Best for:** Advanced users, editing config files, adding raw assets, understanding project structure.

---

### 🧭 Key Differences

| Feature | Android Pane | Project Pane |
|--------|---------------|----------------|
| View Type | Logical (Android-focused) | Actual file system |
| Easy for Beginners | ✅ Yes | 🚫 No |
| Shows all folders | ❌ Only relevant ones | ✅ All |
| Best for | UI, quick coding | Config, assets, advanced tasks |
| Can create custom folders easily | ❌ Limited | ✅ Yes |

---

