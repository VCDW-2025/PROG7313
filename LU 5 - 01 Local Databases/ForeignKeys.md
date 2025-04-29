## Step-by-Step Instructions:

1. **Add `userID` to your `x` entity**  
   - In your `x` data class, include one more property (e.g. `val userId: Int`) alongside other attributes.  
   - Room will automatically persist that integer column.

2. **Extend your DAO with a filter method**  
   - Define a DAO function like `fun getXForUser(userId: Int): List<Donut>` annotated with `@Query("SELECT * FROM donuts WHERE userId = :userId")`.  
   - This returns only the x that belong to a given user.
  
3. **Pass the current user’s ID when querying**  
   - In your fragment or ViewModel, obtain the active user’s primary key (e.g. after login or selection).  
   - Call `xDao.getxForUser(currentUserId)` on a background thread, then submit the list to your RecyclerView adapter.  

4. **Display as usual**  
   - You already have a `RecyclerView` set up for `xAdapter`.  
   - Just give it the filtered list of donuts, and it will show only those created by that user.  

---

### When to add real foreign-keys  
- If you want SQLite to **reject** donuts whose `userId` isn’t in your `User` table, or to **cascade deletes** (removing all a user’s donuts when they’re deleted), add:
  ```kotlin
  @Entity(
    foreignKeys = [
      ForeignKey(
        entity = User::class,
        parentColumns = ["id"],
        childColumns  = ["userId"],
        onDelete      = CASCADE
      )
    ]
  )
  ```
- For a simple app or prototype, the manual-`userId` approach is by far the quickest to implement.
