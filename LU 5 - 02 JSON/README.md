# 💡 **JSON Files**

JSON (JavaScript Object Notation) is a lightweight, human-readable format for storing and transporting data. 

#### 🧾 **Example of a JSON Object**
Imagine you have an order in a coffee app:

```json
{
  "orderId": 9194,
  "customer": "Hope",
  "item": "Latte",
  "size": "Medium",
  "extras": ["Oat Milk", "Vanilla Syrup"],
  "paid": true
}
```

This JSON:
- Uses **curly braces `{}`** to define an object
- Has **keys** like `"customer"`, `"item"`, and `"paid"`
- The **values** can be text (`"Hope"`), numbers (`9194`), booleans (`true`), or even arrays (`["Oat Milk", "Vanilla Syrup"]`)

---

It is widely used in mobile development for:
- Exchanging data between apps and servers (e.g., via REST APIs)
- Saving structured data locally (e.g., user settings, order history)
- Making data easy to read, write, and debug during development

It structures data as **key-value pairs**, and supports **nested objects** and **arrays**, which is ideal for modeling real-world entities like orders, users, or products.
  
#### 🌐 **Example of a REST API using JSON**

A mobile coffee app might call:

```http
GET https://api.coffeeapp.com/orders/1234
```

This fetches order #9194 from the server in JSON format like this:

```json
{
  "orderId": 9194,
  "customer": "Hope",
  "item": "Latte"
}
```

The app could also send a new order using:

```http
POST https://api.coffeeapp.com/orders
```

With JSON data in the request body.

---

## 🛠️ **Activity: Using JSON in Android**

---

### ✅ **1. Use JSON Objects to Read Data**

**Scenario**: Read a `.json` file from your app’s `assets` folder and convert it to Kotlin objects.

**Steps**:

1. Place a file named `orders.json` inside `src/main/assets/`.
2. Create a `data class`:
   ```kotlin
   data class Order(val id: Int, val customer: String, val item: String)
   ```
3. Add Gson to `build.gradle`:
   ```gradle
   implementation 'com.google.code.gson:gson:2.10'
   ```
4. Read the file and parse JSON:
   ```kotlin
   val jsonString = context.assets.open("orders.json").bufferedReader().use { it.readText() }
   val orders = Gson().fromJson(jsonString, Array<Order>::class.java).toList()
   ```

---

### ✅ **2. Use JSON Objects to Write Data**
**Scenario**: Save order data as a JSON string for offline use or transfer.

**Steps**:
1. Create an order object in code:
   ```kotlin
   val newOrder = Order(2, "Hope", "Latte")
   ```
2. Convert to JSON:
   ```kotlin
   val jsonString = Gson().toJson(newOrder)
   ```
3. Save it to SharedPreferences or a file:
   ```kotlin
   val prefs = context.getSharedPreferences("orders", Context.MODE_PRIVATE)
   prefs.edit().putString("last_order", jsonString).apply()
   ```

---

### ✅ **3. Use a Library to Work with JSON Data**
**Gson**, as covered in your manual, is a Google-maintained library that simplifies working with JSON:

- **Deserialise** (JSON → Object):
  ```kotlin
  val order = Gson().fromJson(jsonString, Order::class.java)
  ```

- **Serialise** (Object → JSON):
  ```kotlin
  val jsonString = Gson().toJson(order)
  ```

**Alternative libraries to explore**:
- **Moshi** (built by Square, more modern Kotlin support)
- **Kotlinx.serialization** (native Kotlin serialisation)

---

### 📘 Other JSON Concepts

1. **Handling JSON Arrays**: Students should understand how arrays work in JSON and how to parse them.
2. **Error Handling**: Try-catch around JSON parsing helps avoid crashes from malformed data.
3. **Testing JSON**: Encourage using tools like [JSON Formatter](https://jsonformatter.curiousconcept.com/) to validate and understand structure.
4. **JSON in REST APIs**: Teach how JSON is the backbone of REST responses and requests.
5. **Security and Best Practices**:
   - Avoid exposing sensitive data in JSON (e.g., tokens, passwords)
   - Keep JSON structures flat where possible for performance

