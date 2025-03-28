# 🔗 **Invite Link**

https://classroom.github.com/a/ulHkfFlk

---

# 🎯 Create an Event Management Screen (RecyclerView)

## 📌 What You Will Implement:

📱 **A RecyclerView that lists all events.**

---

### ✏️ **Create an Item Layout File**

Each event should show:

- **Event title**  
- **Date and time**  
- **"Update" button**  
- **"Delete" button**

---

### 🗑️ Delete Functionality

- Clicking **Delete** should remove the event from the **database**.

---

### ✍️ Update Functionality *(Optional for ICE 4)*

- Clicking **Update** should update an event in the **database**.

---

### 📂 Update Your DAO (Data Access Object)

- Add methods to:
  - **Update** an event  
  - **Delete** an event  

---

### 🧩 Create an Adapter Class

- **Extends** `RecyclerView.Adapter`
- Creates an **inner `ViewHolder`** class
- Overrides:
  - `onCreateViewHolder()`  
  - `onBindViewHolder()`  
  - `getItemCount()`  

---

### 📋 Displays a List of `EventEntity` Items

For each item:

- Show the **event title**
- Show the **event date and time**
- Show **Update** and **Delete** buttons

---

### 🧠 Accepts Two Lambda Functions

**When setting up the adapter**, pass:

- `onUpdateClicked`
- `onDeleteClicked`

> These lambdas define what happens when each button is clicked.

**🔸 Why?**  
To keep the adapter **flexible** and **reusable**.

---

### 🔄 Method: `updateEvents()`

- Replaces the current list with a **new one**
- Tells the adapter to **refresh the UI**

**🔸 When to use it?**

- When the database sends **new data**
- Ensures the RecyclerView reflects the **latest state**

---

## 🎯 Final Adapter Should:

- Show a **list of events** with title and date/time  
- Respond to user actions (**update/delete**) using lambdas  
- Automatically **update** when data changes  
- Use **ViewBinding** (instead of `findViewById()`)

---

## ✏️ Implement the `EventManagementActivity`

- Initialise the **AppDatabase**
- Create instance of **`EventsAdapter`**
  - Provide update and delete **lambda logic**
- Set up the RecyclerView with a `LinearLayoutManager`
- **Observe** events from DB → pass to `adapter.updateEvents()`
- Handle **Delete** using **coroutines in `lifecycleScope`**
- For **Update**, show a **Toast** or open a **new screen**
