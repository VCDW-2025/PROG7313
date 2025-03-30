
# 🗄️ **Implement Room for User Management**

---

## 🧩 **Objective**

Integrate the Room persistence library into the MeetMeWhere app to manage user data. In this assignment, you will:
- Create a `UserEntity` that represents a user, using the username as the primary key.
- Implement a Data Access Object (DAO) to write (insert) and read (query) user data.
- Update your `AppDatabase` class to include the new entity.
- Implement a migration to handle schema changes (e.g., when adding a new column or table).
- Modify your registration and login flows to work with the Room database.

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

## 📚 **Resources**

- [Room Persistence Library Documentation](https://developer.android.com/training/data-storage/room)

---

## 🎯 **Evaluation Criteria**

- Correct implementation of `UserEntity` with the username as the primary key.
- Proper functioning of the DAO methods to write and read user data.
- Successful integration of migration to handle schema changes.
- Code clarity, inline comments, and adherence to best practices.

---

This task will help you learn how to manage schema migrations, and perform database operations asynchronously with Kotlin Coroutines. Good luck, and feel free to ask if you have any questions!


