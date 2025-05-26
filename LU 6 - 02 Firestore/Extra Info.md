# 🔍 What is Firestore?

* A NoSQL cloud database by Firebase.
* Stores data as **collections → documents → fields**.
* Realtime updates, offline support, scalable.

### 🏗️ Firestore vs Realtime Database:

| Firestore                          | Realtime DB                   |
| ---------------------------------- | ----------------------------- |
| Structured (collections/documents) | Tree-based JSON               |
| Powerful queries                   | Basic filters                 |
| Offline support                    | Offline support               |
| Better suited for complex apps     | Best for chat, live sync apps |

---

## 2️⃣ **Setting up Firebase in Android Studio**

### 🔧 Step-by-Step:

1. Go to **Tools > Firebase > Firestore**.
2. Click **"Connect to Firebase"** → authenticate Google account.
3. Create or link to an existing Firebase project.
4. Enable **Cloud Firestore** in test mode.
5. Add the Firestore dependency:

```kotlin
implementation("com.google.firebase:firebase-firestore-ktx:24.10.0")
```

6. Add permission to your `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

7. Sync Gradle and initialize Firebase in `Application` or `MainActivity`.

---

## 3️⃣ **Designing the Pet Data Model**

### 🎨 Example Structure for Each Pet:

```json
{
  "name": "Buddy",
  "type": "Dog",
  "age": 3,
  "breed": "Golden Retriever",
  "status": "Available"
}
```

### Kotlin Data Class:

```kotlin
data class Pet(
    val name: String = "",
    val type: String = "",
    val age: Int = 0,
    val breed: String? = null,
    val status: String = "Available"
)
```

---

## 4️⃣ **CRUD Operations in Firestore**

### 📥 Upload/Add Pets

```kotlin
val pet = hashMapOf(
    "name" to "Buddy",
    "type" to "Dog",
    "age" to 3,
    "breed" to "Golden Retriever",
    "status" to "Available"
)

db.collection("adoptable_pets").document("Buddy").set(pet)
```

---

### 📤 Retrieve Pets

```kotlin
db.collection("adoptable_pets").get().addOnSuccessListener { result ->
    for (doc in result) {
        val pet = doc.toObject(Pet::class.java)
        Log.d("Pet", pet.toString())
    }
}
```

---

### 🖊️ Update Pet (Mark Adopted)

```kotlin
db.collection("adoptable_pets").document("Buddy").update("status", "Adopted")
```

---

### ❌ Delete Field

```kotlin
val update = hashMapOf<String, Any>("breed" to FieldValue.delete())
db.collection("adoptable_pets").document("Mittens").update(update)
```

---

### 🗑️ Delete Entire Pet

```kotlin
db.collection("adoptable_pets").document("Buddy").delete()
```

---

## 5️⃣ **Live Walkthrough / Demo (Instructor-led)**

Demonstrate:

1. Uploading 3 pets
2. Viewing them in Firebase Console
3. Retrieving and logging pets
4. Marking a pet as adopted
5. Deleting a field and a document

---

## 6️⃣ **Hands-On Student Activity**

### 👩‍💻 Instructions:

1. Add 3 pets of your own design to Firestore.
2. Retrieve and print them to Logcat.
3. Update one pet’s status.
4. Delete a specific field.
5. Bonus: Add a UI to show pets in a RecyclerView.

---

## 7️⃣ **Bonus: Firestore Rules & Best Practices**

### 🔐 Example Firestore Rules:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /adoptable_pets/{petId} {
      allow read, write: if true; // For testing only
    }
  }
}
```

### 💡 Best Practices:

* Use unique IDs for documents (e.g., pet name + date).
* Avoid deeply nested fields.
* Batch writes if inserting large data.
* Handle null fields carefully with nullable types.

---

