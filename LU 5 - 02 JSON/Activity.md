# Activity

## 🧾 **Coffee Shop Order Manager App**

### ☕ **Context**:
Imagine you're building a mobile app for a **local coffee shop** that wants to manage customer orders.

They want:
1. A way to **store a list of recent customer orders**.
2. The app to **load that list when it opens**, even without internet.
3. The ability to **save new orders** and keep them stored between sessions.

However, the coffee shop doesn’t have a server yet — so they want the app to work **offline** for now, using **local storage**.
---

### 🎯 **Your Task**:
You’ve been hired to build a **prototype version** of the app that does the following:

| Feature | Description |
|--------|-------------|
| ✅ Load orders | From a local file stored in the app (JSON format) |
| ✅ Show order info | Print customer and item details using logs |
| ✅ Create new orders | Directly in code (simulate adding an order) |
| ✅ Save new order | By converting it to JSON and storing it locally |
| ✅ Retrieve saved data | Load saved order from local storage and show it again |

---

### 💡 **Why This Matters (Real-World Relevance)**:

- This mimics how apps like **Uber Eats**, **Starbucks**, or **Takealot** process orders.
- Many apps use **local JSON** for config, offline features, or storing simple data before syncing to the cloud.
- You’re practicing skills needed to:
  - Work with **real APIs**.
  - Handle **local storage and offline support**.
  - Understand **serialisation**, which is a key part of **data communication** in all app development.

---

## ✅ STEP-BY-STEP:

---
### ➤ **Add the Gson Library**

- In your **app-level** `build.gradle`:
  ```gradle
  dependencies {
      implementation ("com.google.code.gson:gson:2.10")
  }
  ```
---

## ✅ STEP 1: Create a JSON Object

### 🔹 **1. Create the `assets/` folder**:
- In the **Project** view:
  - Right-click on `main` → New → Directory → name it `assets`.

### 🔹 **2. Create `orders.json` inside assets**:
- Right-click the new `assets` folder → New → File → name it `orders.json`.

Paste this inside:
```json
[
  { "id": 1, "customer": "Alice", "item": "Cappuccino" },
  { "id": 2, "customer": "Bob", "item": "Espresso" }
]
```

---

## ✅ STEP 2: Create Data Class and Read JSON in Kotlin

### **Create the `Order` data class**
Above the `onCreate()` method in the MainActivity.kt file or in a separate file:

```kotlin
// This defines the structure for each order from the JSON file
data class Order(
    val id: Int,
    val customer: String,
    val item: String
)
```

---

## ✅ STEP 3: Deserialise the JSON object.

📌 Deserialising a JSON object into a Kotlin data class and then outputting the values.

###  **Read the JSON File from Assets**

1. Inside your `MainActivity`, in the `onCreate()` method, open the file `orders.json` using Android’s asset manager.
2. Use a `BufferedReader` to read the entire contents of the file into a single string.

---

### **Convert JSON to Kotlin Objects Using Gson**

1. Use the Gson library to convert the JSON string into a list of your data class objects.
2. Because you're converting a **list**, not just one object, you’ll need to use a helper called `TypeToken`.
3. After the conversion, you’ll have a `List` of order objects in Kotlin.

---

### **Loop Through the List and Display the Orders**

1. Loop through the list of orders.
2. Use Android's `Log.d()` function to print out each order to the **Logcat window**.

> 💡 Think of Log.d() like printing a message to the console, but it goes to Logcat, which is Android's version of a developer console.
---

## ✅ STEP 3: Write Data to JSON (Serialisation) & Save to SharedPreferences

📌 Now that we know how to load data from a file, let’s imagine we want to create a new order in code, convert it to JSON, and save it locally on the device. That way, the next time we open the app, we can read that data back.


### **Create a Kotlin Object**

1. You’re going to manually create a new object using your `Order` class — like you’re simulating a customer placing a new order in the app.
2. The object should include a unique order ID, a customer name, and a coffee item.
3. Store this new object in a variable.

---

### **Serialise the Object to JSON**

1. Use the Gson object (already declared earlier) to convert the order object into a JSON string.
2. Save this JSON string in a variable.

---

### **Save the JSON to SharedPreferences**
1. 
   - Get an instance of SharedPreferences.
   - Use the `edit()` function and save the JSON string under a key (e.g., `"last_order"`).
   - Apply the changes.

---

### **Read the Saved JSON Back (Deserialisation)**

📌 The app just restarted. We want to get the last saved order and use it again.

1.
   - Get the JSON string from SharedPreferences using the key they used earlier.
   - Check that it’s not `null` (to avoid crashes).
   - Use Gson to convert the JSON string back into an `Order` object.

---

### **Display or Log the Restored Order**
1. Use `Log.d()` to output the order’s customer name and item in Logcat, to confirm it was successfully restored.

---

