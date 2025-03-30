# 🗄️ **Local Databases**

---

## 🧩 What is a Local Database?

A **local database** stores data directly on the user's device. It allows your app to **save, retrieve, update, and delete data** even without internet access.

---

## 🧩 Why Use a Local Database?

- To **store user data offline**
- To **persist app state** (e.g., saved items, preferences)
- To **cache network data**
- To **track usage history** or logs

---

## 🧩 Common Local Databases in Android

### 📕 **1. Room (SQLite wrapper)**

- A Jetpack library that simplifies SQLite
- Uses **annotations** instead of raw SQL
- Handles object mapping (ORM = Object Relational Mapping)

### 📘 **2. SQLite**

- Lightweight, relational database
- Built into Android
- You use SQL queries to create tables, insert and query data

---

## 🧩 Key Components of Room

### 🧾 Entity

- A data class that represents a **table**

```kotlin
@Entity
data class User(
    @PrimaryKey val id: Int,
    val name: String
)
```

### 📚 DAO (Data Access Object)
- Interface with methods for querying the database

```kotlin
@Dao
interface UserDao {
    @Query("SELECT * FROM user")
    fun getAll(): List<User>

    @Insert
    fun insert(user: User)
}
```

### 🏠 Database

- Abstract class that connects everything together

```kotlin
@Database(entities = [User::class], version = 1)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
}
```

---

### 🎯 Summary

| Tool             | Best For                          |
|------------------|-----------------------------------|
| SQLite           | Full control, raw SQL             |
| Room             | Simplified SQLite + annotations   |
| SharedPreferences| Simple settings, key-value pairs  |
| DataStore        | Modern key-value or typed storage |

---

## 🧩 How to implement Room

Folders for implementing room to events and users are above.


