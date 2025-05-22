# 🔥**Fire Store**

Firestore, officially called **Cloud Firestore**, is a NoSQL cloud database from Google that's part of **Firebase**, used to store and sync data for web and mobile apps in real time.

## 🧩 1. **Database Structure**

Firestore is **document-based**, not relational like SQL. Its hierarchy looks like this:

```
Firestore
└── Collection
    └── Document
        └── Fields (key-value pairs)
        └── Subcollections (optional)
```

* **Collection**: A container for documents (e.g., `users`, `posts`).
* **Document**: A record in a collection, stored as a JSON-like object with fields (e.g., `name: "Emma"`, `age: 25`).
* **Fields**: Data inside a document.
* **Subcollections**: You can nest collections inside documents.

✅ Example:

```
users (collection)
 └── userId123 (document)
     ├── name: "Emma"
     ├── age: 25
     └── orders (subcollection)
          └── orderId456 (document)
              ├── item: "Coffee"
              ├── price: 45.00
```

---

## 🔄 2. **Real-time Sync**

Whenever data changes in Firestore:

* Listeners in your app **automatically receive updates** in real time.
* This is ideal for apps like chats, dashboards, or collaborative tools.

---

## ☁️ 3. **Offline Support**

Firestore caches data locally:

* Your app can still read/write while offline.
* Once online, it syncs automatically with the cloud.

---

## 🔐 4. **Security Rules**

Firestore uses **Firebase Security Rules** to:

* Restrict who can **read or write** data.
* Enforce logic like: “Only allow users to edit their own documents.”

Example:

```plaintext
match /users/{userId} {
  allow read, write: if request.auth.uid == userId;
}
```

---

## 🔍 5. **Querying**

You can query collections with filters and ordering:

```kotlin
// Kotlin / Android
val db = FirebaseFirestore.getInstance()
db.collection("users")
  .whereEqualTo("age", 25)
  .orderBy("name")
  .get()
```

⚠️ Firestore supports compound queries, but indexes may be needed.

---

## 🔥 6. **Integration in Android**

You typically:

* Add Firebase SDKs to your Android project.
* Initialize Firestore (`FirebaseFirestore.getInstance()`).
* Use listeners (`addSnapshotListener`) or one-time reads (`get()`).
* Use `DocumentReference` and `CollectionReference` for operations.





