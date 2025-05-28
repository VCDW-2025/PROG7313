## ✅ **1. Set Up Firebase in Your Project**

Before replacing RoomDB:

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Add your Android app to a Firebase project.
3. Download the `google-services.json` file and place it in your app module (`/app`).
4. Add the following to your `build.gradle.kts` (or `build.gradle`) files:

**Project-level:**

```kotlin
classpath("com.google.gms:google-services:4.4.0") // or latest
```

**App-level:**

```kotlin
plugins {
    id("com.google.gms.google-services")
}

dependencies {
    implementation("com.google.firebase:firebase-firestore-ktx")
}
```

---

## ✅ **2. Remove RoomDB Dependencies**

Remove these from your build.gradle:

```kotlin
// REMOVE:
implementation("androidx.room:room-runtime")
kapt("androidx.room:room-compiler")
```

---

## ✅ **3. Replace Room Entities with Firestore Data Models**

Room uses `@Entity`, but Firestore just needs **plain Kotlin data classes**.

**Room:** Eg:

```kotlin
@Entity(tableName = "expenses")
data class Expense(
    @PrimaryKey(autoGenerate = true) val id: Int,
    val name: String,
    val amount: Float
)
```

**Firestore:** Eg:

```kotlin
data class Expense(
    val name: String = "",
    val amount: Float = 0f
)
```

* No annotations required.
* Must include default values (important for Firestore deserialization).

---

## ✅ **4. Replace DAO Operations with Firestore Code**

Room example:

```kotlin
expenseDao.insert(Expense("Taxi", 100f))
```

Firestore equivalent:

```kotlin
val db = Firebase.firestore
db.collection("expenses").add(Expense("Taxi", 100f))
```

---

### 🧠 Important Notes

* Firestore is **NoSQL**, so there’s no concept of joins. Denormalize your data.
* Room operations are local. Firestore is **cloud-based**, so it requires internet (but you can enable offline mode).
* You don’t need `LiveData` for Firestore — it has **snapshot listeners**.

---
