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

You can safely **delete your DAO files**. But do so **only after**:

### You’ve Done the Following:

1. **Replaced all Room database operations** in your app with Firestore equivalents:

   * `insert()` → `collection().add()`
   * `getAll()` → `collection().get()`
   * `update()` → `document().update()`
   * `delete()` → `document().delete()`

2. **Removed Room annotations** (e.g., `@Dao`, `@Insert`, `@Query`) and data access logic from your codebase.

3. **Tested Firestore read/write** across your entire app to make sure it works without Room.

---

### 🔥 When You Can Delete DAO Files

If:

* You’ve removed all Room-related code from your ViewModels, Repositories, and Activities/fragments
* Your Firestore setup works consistently
* You’ve removed Room dependencies from `build.gradle`

Then:
**You can delete your DAO interfaces (`ExpenseDao.kt`, etc.) and any `RoomDatabase` subclass (`AppDatabase.kt`).**

---

### 🧠 Important Notes

* Firestore is **NoSQL**, so there’s no concept of joins. Denormalize your data.
* Room operations are local. Firestore is **cloud-based**, so it requires internet (but you can enable offline mode).
* You don’t need `LiveData` for Firestore — it has **snapshot listeners**.

---
