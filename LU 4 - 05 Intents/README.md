# 🫧 **Intents**

An **Intent** is a messaging object in Android that allows you to **request an action** from another component — like opening a new screen, sending a message, launching the camera, etc.

---

## 📌 **Why Use Intents?**

Intents help your app:
- Move between **activities** (screens)
- Start a **service**
- Launch another **app**
- Send or receive **data**

---

## 📌 **Two Main Types of Intents**

| Type              | Purpose |
|-------------------|---------|
| **Explicit Intent** | Start a specific component in *your own app*. |
| **Implicit Intent** | Request an action that *any capable app* can handle. |

---

## ✅ **1. Explicit Intent (Same App)**

### ⚙️ Example: 

Move from `MainActivity` to `SecondActivity`

```kotlin
val intent = Intent(this, SecondActivity::class.java)
startActivity(intent)
```

### ⚙️ With Data:

```kotlin
val intent = Intent(this, SecondActivity::class.java)
intent.putExtra("USERNAME", "jungkook")
startActivity(intent)
```

In `SecondActivity.kt`:

```kotlin
val username = intent.getStringExtra("USERNAME")
```

---

## 🌐 **2. Implicit Intent (Across Apps)**

### ⚙️ Open a Website:

```kotlin
val intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("https://www.google.com")
startActivity(intent)
```

### 📞 Make a Call:

```kotlin
val intent = Intent(Intent.ACTION_DIAL)
intent.data = Uri.parse("tel:123456789")
startActivity(intent)
```

### 📤 Share Text:

```kotlin
val intent = Intent(Intent.ACTION_SEND)
intent.type = "text/plain"
intent.putExtra(Intent.EXTRA_TEXT, "Hello from my app!")
startActivity(Intent.createChooser(intent, "Share via"))
```

---

## 🔨 **Extra Features**

| Feature | Use |
|--------|-----|
| `putExtra()` | Attach data to send |
| `getStringExtra()` / `getIntExtra()` | Retrieve data in the next activity |
| `startActivityForResult()` | Get a result back from an activity (now replaced by Activity Result API) |

---

## 🎯 Summary

| Feature | Explicit Intent | Implicit Intent |
|---------|------------------|------------------|
| Used for | In-app navigation | External actions |
| Needs component name | ✅ Yes | ❌ No |
| Common in | Switching screens | Calling, sharing, viewing links |


