# 🤳**SQLite**

**Room Database** (RoomDB) is a wrapper around **SQLite** in Android. It simplifies database interactions and provides a higher-level abstraction over SQLite.

Room provides an easier way to handle SQLite operations by eliminating much of the boilerplate code needed for CRUD (Create, Read, Update, Delete) operations.

## Relation to SQLite:

1. **SQLite Foundation**: Room uses SQLite as its underlying database. It leverages SQLite to store and manage data in a local database on the device.

2. **Abstraction Layer**: Room adds an abstraction layer over SQLite, providing a more convenient API. It allows developers to interact with the database using objects (via **DAO - Data Access Objects**) instead of writing raw SQL queries.

3. **Data Persistence**: Like SQLite, Room persists data in tables. However, Room converts your Java or Kotlin objects into SQLite rows using annotations like `@Entity`, `@Dao`, and `@Database`.

4. **Automatic SQL Generation**: Room automatically generates the necessary SQL queries for basic CRUD operations based on the annotations you provide. It also handles database schema migrations, which can be a complex task when working directly with SQLite.

