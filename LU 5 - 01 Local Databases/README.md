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

### 📘 **1. SQLite**

- Lightweight, relational database
- Built into Android
- You use SQL queries to create tables, insert and query data

### 📕 **2. Room (SQLite wrapper)**

- A Jetpack library that simplifies SQLite
- Uses **annotations** instead of raw SQL
- Handles object mapping (ORM = Object Relational Mapping)

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

Below is an assignment prompt with step-by-step instructions for your students to implement Room in the MeetMeWhere app—specifically focusing on writing (inserting) and reading events from the database.

---

### **Implement Room for Event Data**

**Objective:**  
Integrate the Room persistence library into your MeetMeWhere app to store event details. You will create an EventEntity to represent events, implement DAO methods to write and read events from the database, and update the UI to reflect the stored data.

---

### **Tasks:**

1. **Define an Event Entity:**
   - Create a Kotlin data class named `EventEntity`.
   - Annotate it with `@Entity(tableName = "events")`.
   - Include fields such as `id` (primary key with auto-generation), `title`, `description`, `date`, `time`, and `location`.

   *Example:*
   ```kotlin
   @Entity(tableName = "events")
   data class EventEntity(
       @PrimaryKey(autoGenerate = true)
       val id: Int = 0,
       val title: String,
       val description: String,
       val date: String,
       val time: String,
       val location: String
   )
   ```

2. **Create a Data Access Object (DAO):**
   - Create an interface called `EventDao`.
   - Add an `@Insert` method to write (insert) an event into the database.
   - Add an `@Query` method to read (retrieve) all events from the database as a LiveData list.

   *Example:*
   ```kotlin
   @Dao
   interface EventDao {
       @Insert
       suspend fun insertEvent(event: EventEntity): Long

       @Query("SELECT * FROM events")
       fun getAllEvents(): LiveData<List<EventEntity>>
   }
   ```

3. **Set Up the Room Database:**
   - Create or update your `AppDatabase` class to include the `EventEntity` and the `EventDao`.
   - Use the `@Database` annotation and specify the version number.
   - Implement a singleton pattern in the companion object to create and retrieve the database instance.

   *Example:*
   ```kotlin
   @Database(entities = [EventEntity::class], version = 1, exportSchema = false)
   abstract class AppDatabase : RoomDatabase() {
       abstract fun eventDao(): EventDao

       companion object {
           @Volatile
           private var INSTANCE: AppDatabase? = null

           fun getDatabase(context: Context): AppDatabase {
               return INSTANCE ?: synchronized(this) {
                   val instance = Room.databaseBuilder(
                       context.applicationContext,
                       AppDatabase::class.java,
                       "meetmewhere_database"
                   ).build()
                   INSTANCE = instance
                   instance
               }
           }
       }
   }
   ```

4. **Write Event Data to the Database:**
   - In your Event Creation screen (e.g., `EventCreationActivity`), retrieve input from the user for the event details.
   - Use Kotlin coroutines (e.g., `lifecycleScope.launch { ... }`) along with `withContext(Dispatchers.IO)` to insert the event using the DAO method.
   - Display a Toast message to indicate success or error.

   *Example Code Snippet:*
   ```kotlin
   lifecycleScope.launch {
       try {
           withContext(Dispatchers.IO) {
               db.eventDao().insertEvent(newEvent)
           }
           Toast.makeText(this@EventCreationActivity, "Event Saved: ${newEvent.title}", Toast.LENGTH_SHORT).show()
       } catch (e: Exception) {
           e.printStackTrace()
           Toast.makeText(this@EventCreationActivity, "Error saving event: ${e.message}", Toast.LENGTH_LONG).show()
       }
   }
   ```

5. **Read Event Data from the Database:**
   - In your Event Management screen (or fragment), set up a RecyclerView to display the list of events.
   - Observe the LiveData returned by `getAllEvents()` in your DAO. When the data changes, update the RecyclerView adapter to display the events.
   - Use a ViewModel to hold the LiveData if you prefer separation of concerns, or observe directly from the Activity.

   *Example Code for Observing LiveData:*
   ```kotlin
   // In your EventManagementActivity or fragment:
   db.eventDao().getAllEvents().observe(this) { events ->
       adapter.updateEvents(events)
   }
   ```

6. **Documentation & Testing:**
   - Provide comments in your code explaining each part of your Room integration.
   - Test the app by creating events, verifying they are saved to the database, and confirming that the Event Management screen displays the list of events.
   - If you make changes to your schema, remember to update the version number or clear app data to force a rebuild of the database.

---

### **Deliverables:**

- Updated code implementing the EventEntity, EventDao, and AppDatabase.
- Modified Event Creation and Event Management screens that write to and read from the Room database.
- A short report (1–2 pages) explaining your implementation, including screenshots demonstrating event insertion and retrieval.
- Well-commented code that explains the use of key libraries:
  - **Room:** For local data persistence.
  - **LiveData:** For observing database changes.
  - **Kotlin Coroutines (Dispatchers.IO and lifecycleScope):** For performing database operations off the main thread.
  - **ViewBinding:** For simplified and type-safe view access.

---


---

# 🗄️ **Assignment: Implement Room for User Management**

---

## 🧩 **Objective**

Integrate the Room persistence library into the MeetMeWhere app to manage user data. In this assignment, you will:
- Create a `UserEntity` that represents a user, using the username as the primary key.
- Implement a Data Access Object (DAO) to write (insert) and read (query) user data.
- Update your `AppDatabase` class to include the new entity.
- Implement a migration to handle schema changes (e.g., when adding a new column or table).
- Modify your registration and login flows to work with the Room database.

---

## 🧩 **Why Use Room?**

- **Simplified Database Access:** Room uses annotations to reduce boilerplate and provide compile-time verification of SQL queries.
- **LiveData Integration:** Easily observe data changes to automatically update your UI.
- **Safe Threading:** Room works with Kotlin Coroutines to perform database operations off the main thread.
- **Schema Migrations:** Room supports schema migrations, so you can evolve your database without losing user data.

---

## 🧩 **Instructions**

### 1. Define the User Entity

Create a Kotlin data class called `UserEntity` that represents a user in your database. The username will serve as the primary key.

- **File:** `UserEntity.kt`
- **Requirements:**
  - Annotate with `@Entity(tableName = "users")`.
  - Use `@PrimaryKey` on the username field.
  - Include at least two fields: `username` and `password`.

*Example:*
```kotlin
package com.talia.meetmewheregroup2

import androidx.room.Entity
import androidx.room.PrimaryKey

// Define the users table where the username is the primary key.
@Entity(tableName = "users")
data class UserEntity(
    @PrimaryKey
    val username: String,  // Primary key for the table.
    val password: String   // User password.
)
```

---

### 2. Create the User DAO

Create an interface `UserDao` that defines methods for inserting a user and querying a user by username.

- **File:** `UserDao.kt`
- **Requirements:**
  - An `@Insert` method for adding a user.
  - An `@Query` method to retrieve a user by username.

*Example:*
```kotlin
package com.talia.meetmewheregroup2

import androidx.room.Dao
import androidx.room.Insert
import androidx.room.Query

@Dao
interface UserDao {
    // Inserts a new user into the database.
    @Insert
    suspend fun insertUser(user: UserEntity): Long

    // Retrieves a user from the database by username.
    @Query("SELECT * FROM users WHERE username = :username LIMIT 1")
    suspend fun getUserByUsername(username: String): UserEntity?
}
```

---

### 3. Set Up the Room Database with Migration

Update or create your `AppDatabase` class to include the new `UserEntity` and `UserDao`. Also, implement a migration to handle schema changes if needed.

- **File:** `AppDatabase.kt`
- **Requirements:**
  - Annotate with `@Database(entities = [UserEntity::class, ...], version = 2, exportSchema = false)`.
  - Implement a singleton pattern for the database instance.
  - Define a migration object (e.g., `MIGRATION_1_2`) that creates the `users` table if it didn’t exist in version 1.

*Example:*
```kotlin
package com.talia.meetmewheregroup2

import android.content.Context
import androidx.room.Database
import androidx.room.Room
import androidx.room.RoomDatabase
import androidx.room.migration.Migration
import androidx.sqlite.db.SupportSQLiteDatabase

// Include UserEntity (and any other entities, e.g., EventEntity) in the database.
// Update the version number when changes occur.
@Database(entities = [UserEntity::class /*, EventEntity::class*/], version = 2, exportSchema = false)
abstract class AppDatabase : RoomDatabase() {
    abstract fun userDao(): UserDao
    // If using other DAOs, e.g., eventDao, declare them here.

    companion object {
        @Volatile
        private var INSTANCE: AppDatabase? = null

        // Migration from version 1 to 2: Create the 'users' table.
        val MIGRATION_1_2 = object : Migration(1, 2) {
            override fun migrate(database: SupportSQLiteDatabase) {
                // Create the 'users' table with the username as primary key.
                database.execSQL(
                    """
                    CREATE TABLE IF NOT EXISTS `users` (
                        `username` TEXT NOT NULL,
                        `password` TEXT NOT NULL,
                        PRIMARY KEY(`username`)
                    )
                    """.trimIndent()
                )
            }
        }

        // Function to get the database instance, applying the migration.
        fun getDatabase(context: Context): AppDatabase {
            return INSTANCE ?: synchronized(this) {
                val instance = Room.databaseBuilder(
                    context.applicationContext,
                    AppDatabase::class.java,
                    "meetmewhere_database"
                )
                    .addMigrations(MIGRATION_1_2)  // Apply the migration from version 1 to 2.
                    .build()
                INSTANCE = instance
                instance
            }
        }
    }
}
```

---

### 4. Write User Data to the Database

In your registration flow (e.g., `RegisterActivity`), use Kotlin Coroutines to insert a new user into the Room database.

- **Use `lifecycleScope.launch`** to run a coroutine tied to the Activity's lifecycle.
- **Switch to `Dispatchers.IO`** for the database operation to avoid blocking the main thread.
- **Example Code:**
```kotlin
lifecycleScope.launch {
    try {
        // Check if the username already exists.
        val existingUser = withContext(Dispatchers.IO) {
            userDao.getUserByUsername(username)
        }
        if (existingUser != null) {
            Toast.makeText(this@RegisterActivity, "Username already exists", Toast.LENGTH_SHORT).show()
        } else {
            // Insert new user into the database.
            val newUser = UserEntity(username = username, password = password)
            withContext(Dispatchers.IO) {
                userDao.insertUser(newUser)
            }
            Toast.makeText(this@RegisterActivity, "Registration successful!", Toast.LENGTH_SHORT).show()
            // Navigate to the next screen as needed.
        }
    } catch (e: Exception) {
        e.printStackTrace()
        Toast.makeText(this@RegisterActivity, "Error: ${e.message}", Toast.LENGTH_LONG).show()
    }
}
```

---

### 5. Read User Data from the Database

In your login flow (e.g., `MainActivity`), query the Room database for a user by their username to verify login credentials.

- **Use `lifecycleScope.launch`** and `withContext(Dispatchers.IO)` for the query.
- **Example Code:**
```kotlin
lifecycleScope.launch {
    // Retrieve the user from the database using their username.
    val user = withContext(Dispatchers.IO) {
        userDao.getUserByUsername(username)
    }
    if (user == null) {
        Toast.makeText(this@MainActivity, "User not found", Toast.LENGTH_SHORT).show()
    } else {
        // Compare the provided password with the stored password.
        if (user.password == password) {
            // Credentials are valid.
            val intent = Intent(this@MainActivity, EventManagementActivity::class.java)
            intent.putExtra("username", username)
            startActivity(intent)
        } else {
            Toast.makeText(this@MainActivity, "Invalid credentials", Toast.LENGTH_SHORT).show()
        }
    }
}
```

---

## 📝 **Deliverables**

- Updated code files:
  - `UserEntity.kt`
  - `UserDao.kt`
  - `AppDatabase.kt` (with migration implementation)
  - Updated registration and login flows to write and read user data.
- A short report (1–2 pages) explaining your implementation:
  - How you implemented Room for user management.
  - How the migration works.
  - Screenshots demonstrating successful user registration and login.
- Well-commented code that explains:
  - How Room, LiveData, and Kotlin Coroutines are used.
  - The role of each component (Entity, DAO, Database, Migration).

---

## 📚 **Resources**

- [Room Persistence Library Documentation](https://developer.android.com/training/data-storage/room)

---

## 🎯 **Evaluation Criteria**

- Correct implementation of `UserEntity` with the username as the primary key.
- Proper functioning of the DAO methods to write and read user data.
- Successful integration of migration to handle schema changes.
- Code clarity, inline comments, and adherence to best practices.
- A concise report that explains your approach and includes screenshots.

---

This assignment will help you learn how to manage schema migrations, and perform database operations asynchronously with Kotlin Coroutines. Good luck, and feel free to ask if you have any questions!




