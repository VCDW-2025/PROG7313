## 1. Enable KAPT  
You must apply the Kotlin annotation-processing tool (KAPT) so Room’s annotations can generate the necessary boilerplate during compilation 🏷️.

---

## 2. Add Room Dependencies  
Include Room’s runtime library, its compiler for annotation processing, and the Kotlin extensions for coroutine support in your Gradle setup 📦.

---

## 3. Define Your Entity  
Create a plain Kotlin data class representing a Donut and annotate it so Room knows to map it to a database table. Each property becomes a column, with one marked as the primary key.  

---

## 4. Create a DAO Interface  
Define an interface with methods to insert new donuts and query existing ones. Annotate these methods (e.g., `@Insert`, `@Query`) so Room will auto-generate the underlying SQL and implementation. 

---

## 5. Build the Room Database  
Make an abstract class extending RoomDatabase, listing your entity and DAO in its annotation so Room can wire them together. Expose a thread-safe singleton getter to obtain the database instance from your application context. 

---

## 6. Work with Image URIs  
When the user picks an image, Android returns a content URI (e.g. `content://…`). Convert that URI to a string and store it in your entity’s `imageUri` field. Later, parse it back to an Android `Uri` and feed it to your `ImageView` or an image-loading library, which resolves the actual bytes via a ContentProvider under the hood 🔄.  

---

## 7. Perform Inserts on a Background Thread  
Never write to the database on the main thread. Launch a coroutine on an I/O dispatcher to call your DAO’s insert method, then switch back to the main dispatcher to update the UI (e.g., show a confirmation). 

---

