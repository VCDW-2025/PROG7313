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





