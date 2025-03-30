
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
   - In your Event Management screen, set up a RecyclerView to display the list of events.
   - Observe the LiveData returned by `getAllEvents()` in your DAO. When the data changes, update the RecyclerView adapter to display the events.
   - Use a ViewModel to hold the LiveData if you prefer separation of concerns, or observe directly from the Activity.

   *Example Code for Observing LiveData:*
   ```kotlin
   // In your EventManagementActivity:
   db.eventDao().getAllEvents().observe(this) { events ->
       adapter.updateEvents(events)
   }
   ```

---

